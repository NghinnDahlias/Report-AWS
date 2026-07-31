---
title: "Prepare EC2 and IAM Role"
weight: 1
chapter: false
pre: " <b> 5.7.1. </b> "
---

#### Create the IAM role for the backend

1. Open the **AWS Management Console**.
2. Search for and open **IAM**.
3. In the left navigation, choose **Roles**.
4. Choose **Create role**.
5. Under **Trusted entity type**, choose **AWS service**.
6. Under **Use case**, choose **EC2**.
7. Choose **Next**.

Attach `AmazonSSMManagedInstanceCore` so the EC2 instance can be managed through AWS Systems Manager Session Manager.

Then create the runtime policy for the backend:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "SubscriberTable",
      "Effect": "Allow",
      "Action": [
        "dynamodb:GetItem",
        "dynamodb:PutItem",
        "dynamodb:UpdateItem",
        "dynamodb:Scan"
      ],
      "Resource": "arn:aws:dynamodb:ap-southeast-1:ACCOUNT_ID:table/local-aqi-subscribers-dev"
    },
    {
      "Sid": "AlertTopic",
      "Effect": "Allow",
      "Action": [
        "sns:GetSubscriptionAttributes",
        "sns:ListSubscriptionsByTopic",
        "sns:Publish",
        "sns:Subscribe"
      ],
      "Resource": "arn:aws:sns:ap-southeast-1:ACCOUNT_ID:local-aqi-alerts-dev"
    },
    {
      "Sid": "ForecastEndpoint",
      "Effect": "Allow",
      "Action": "sagemaker:InvokeEndpoint",
      "Resource": "arn:aws:sagemaker:ap-southeast-1:ACCOUNT_ID:endpoint/ENDPOINT_NAME"
    }
  ]
}
```

Replace `ACCOUNT_ID` and `ENDPOINT_NAME` with the real deployment values.

Use the role name:

```text
local-aqi-backend-ec2-role
```

#### Create the Security Group

1. Open **Amazon EC2**.
2. In the left navigation, choose **Security Groups**.
3. Choose **Create security group**.
4. Enter the name:

```text
local-aqi-backend-sg
```

5. Choose the VPC used by the project.
6. Add the following inbound rule:

| Type | Protocol | Port range | Source |
| --- | --- | --- | --- |
| Custom TCP | TCP | `8000` | My IP or the CIDR approved for the demo |

Do not open SSH port `22`. Instance administration should be handled through Session Manager.

#### Launch the EC2 instance

1. In **Amazon EC2**, choose **Instances**.
2. Choose **Launch instances**.
3. Enter the instance name:

```text
local-aqi-dev-ec2-backend
```

4. Choose an Amazon Linux AMI.
5. Choose an instance type suitable for the demo environment, for example `t3.micro`.
6. Under **Key pair**, choose **Proceed without a key pair**.
7. Select the `local-aqi-backend-sg` Security Group.
8. Under **Advanced details**, attach the IAM instance profile for `local-aqi-backend-ec2-role`.
9. Enable **IMDSv2**.
10. Use an encrypted `gp3` EBS volume and enable delete-on-terminate.

Add the following tags:

```text
Project=local-aqi-forecasting
Environment=dev
Owner=quang-tuan
Module=backend
```

After the instance reaches `Running` and appears in Systems Manager, continue to the installation step.
