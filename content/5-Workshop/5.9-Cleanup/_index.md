---
title : "Cleanup and Resource Teardown"
date : 2026-07-31
weight : 9
chapter : false
pre : " <b> 5.9. </b> "
---

#### Role objective

This section explains how the team shut down AWS resources after the workshop demo to avoid unnecessary cost while keeping the evidence and outputs needed for the final report.

#### Cleanup goals

+ Back up the required raw data, processed data, and outputs
+ Stop or delete compute resources that continue to incur cost
+ Remove integration resources that are no longer needed
+ Verify that no unexpected AWS charges remain after teardown

#### Suggested cleanup flow

1. Back up the required evidence from Amazon S3 and local outputs.
2. Delete the SageMaker endpoint, endpoint configuration, and model if they are no longer needed.
3. Stop or terminate the EC2 instance used for the FastAPI backend.
4. Remove IoT Rule, Firehose delivery stream, and related temporary integration resources.
5. Delete SNS topics or subscriptions that were created only for the demo.
6. Clean up S3 objects and buckets only after the necessary files have been saved.
7. Review CloudWatch logs, IAM roles, Elastic IP, and other leftover billable resources.
8. Check AWS Billing and Budgets one more time after teardown.

#### Resources that usually need review

+ Amazon SageMaker Endpoint
+ Amazon EC2 Instance
+ Amazon Data Firehose
+ AWS IoT Core Rule
+ Amazon SNS Topic and Subscription
+ Amazon S3 Buckets
+ Amazon CloudWatch Log Groups
+ IAM roles created specifically for the project

#### Expected outcome

After cleanup, the account should no longer keep unnecessary workshop resources running, and the team should still retain the architecture screenshots, logs, datasets, and outputs needed for documentation and presentation.

{{% notice note %}}
Delete S3 buckets, IAM roles, and IoT certificates only after confirming that all report evidence and demo artifacts have already been backed up.
{{% /notice %}}
