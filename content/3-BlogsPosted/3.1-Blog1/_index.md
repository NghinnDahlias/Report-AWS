---
title: "Blog 1"
date: 2026-07-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

{{% notice warning %}}
**Note:** The information below is for reference purposes only. Please **do not copy it verbatim** into your report.
{{% /notice %}}

# WHY DOES AN IAM ROLE WITH AWS SERVICE PERMISSIONS STILL NOT WORK?

While working with AWS from a DevOps perspective during the internship, one of the areas that took me the most time to debug was access configuration between AWS services.

At first, I assumed that creating an IAM role, attaching the required permissions, and selecting that role for a service would be enough to make the system work. In practice, however, a role can appear to have the right permissions and still fail when used by an AWS service.

The root cause usually lies in three separate pieces:

* Trust Policy
* Permission Policy
* The `iam:PassRole` permission of the person configuring the resource

## Core concepts to understand

### Trust Policy

A trust policy defines which principal is allowed to use or assume an IAM role.

In simple terms:

> A trust policy answers the question: "Who is allowed to use this role?"

For example, if a specific AWS service needs to use a role:

```json
{
  "Version": "2026-07-01",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "service-a.amazonaws.com"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
```

If the service principal is declared incorrectly, the service will not be able to use the role, even if the role already has the required permissions.

### Permission Policy

A permission policy defines what actions the role is allowed to perform on which resources after it has been assumed.

In simple terms:

> A permission policy answers the question: "After using the role, what is it allowed to do?"

For example:

```json
{
  "Version": "2026-07-01",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "service-b:WriteData",
      "Resource": "arn:aws:service-b:region:123456789012:resource/example"
    }
  ]
}
```

A service role only works correctly when both the trust policy and the permission policy are configured properly.

```text
Correct Trust Policy
        +
Correct Permission Policy
        =
The AWS service can use the role
```

## What is `iam:PassRole`?

Another common issue is when a user can create or configure an AWS resource but cannot select the IAM role that the resource needs.

When a user chooses a role for an AWS service, that user does not directly assume the role. Instead, the system passes the role to the service through:

```text
iam:PassRole
```

For example, a policy that limits the right to pass one specific role:

```json
{
  "Version": "2026-07-01",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "iam:PassRole",
      "Resource": "arn:aws:iam::123456789012:role/example-service-role",
      "Condition": {
        "StringEquals": {
          "iam:PassedToService": "service-a.amazonaws.com"
        }
      }
    }
  ]
}
```

It is not a good practice to grant broad access like:

```json
{
  "Effect": "Allow",
  "Action": "iam:PassRole",
  "Resource": "*"
}
```

Overly broad `iam:PassRole` permissions can allow a user to attach a far more powerful role to an AWS service than their job actually requires.

## The difference between `iam:PassRole` and `sts:AssumeRole`

These two actions are often confused, but they serve different purposes.

### `sts:AssumeRole`

Used when a user, application, or AWS service directly receives temporary credentials from a role.

```text
Principal
-> AssumeRole
-> Receive temporary credentials
-> Perform actions allowed by the role
```

### `iam:PassRole`

Used when a person configures an AWS resource and selects a role for an AWS service to use.

```text
Configurator
-> PassRole
-> AWS service receives the role
-> AWS service assumes the role
```

In short:

```text
AssumeRole:
The principal directly uses the role.

PassRole:
The principal hands the role to an AWS service.
```

## Checklist when an AWS service cannot use an IAM role

When I run into role-related errors, instead of granting broader permissions immediately, I usually verify the following in order:

* Is the trust policy using the correct service principal?
* Does the permission policy include the required actions?
* Are the ARNs correct for the target account, region, and resource?
* Does the person configuring the resource have `iam:PassRole`?
* Does that `iam:PassRole` permission apply to the exact role being used?
* Is the `iam:PassedToService` condition correct?
* Is the role restricted by a permissions boundary?
* Is there an explicit deny from another policy?

General troubleshooting flow:

```text
Configurator
-> Has PassRole permission
-> AWS service is trusted
-> Service assumes the role
-> Role has the required permissions
-> Target resource accepts the request
```

## Lessons learned

Before working on real AWS deployments, I usually pictured IAM in a very simple flow:

```text
User
-> Policy
-> Permission
```

After going through real implementation scenarios, I realized that permission delegation between AWS services includes many more layers:

```text
Configurator
-> Passes the role to an AWS service
-> The AWS service is allowed to assume the role
-> The role performs the permitted actions
-> The target resource receives the request
```

That is why, when a role does not work, checking only the permission policy is not enough.

The three most important questions are:

* Trust Policy: Who is allowed to use the role?
* Permission Policy: What is the role allowed to do?
* `iam:PassRole`: Who is allowed to hand that role to an AWS service?

## Applying the principle of least privilege

Instead of attaching very broad policies such as:

```text
AdministratorAccess
IAMFullAccess
AmazonS3FullAccess
```

DevOps engineers should narrow access based on:

* specific actions
* specific IAM roles
* specific AWS services
* specific resource ARNs
* specific deployment environments

For example:

```text
Not recommended:
iam:PassRole on every role.

Recommended:
iam:PassRole on one specific role,
combined with a restriction on which service can receive it.
```

This still allows team members to complete their work while reducing the risk of accidental misuse or privilege escalation.

## Conclusion

The most important lesson I learned is:

> An IAM role having permissions does not guarantee that AWS can actually use it. The service must be trusted by the trust policy, and the person configuring the resource may also need `iam:PassRole`.

IAM is not just about granting permissions so that a system can run. A good IAM design must clearly define:

```text
Who
-> can use which role
-> to perform which actions
-> on which resources
```

Understanding the relationship between trust policies, permission policies, and `iam:PassRole` helps speed up debugging, reduces the temptation to grant overly broad permissions, and supports least-privilege design much more effectively.

## References

* [AWS IAM Roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html)
* [Grant a user permissions to pass a role to an AWS service](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_passrole.html)
* [IAM Policies and Permissions](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html)
* [IAM Security Best Practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)
* [Troubleshooting IAM Roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/troubleshoot_roles.html)
