---
title: "Blog 3"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---

{{% notice warning %}}
**Note:** The information below is for reference purposes only. Please **do not copy it verbatim** into your report.
{{% /notice %}}

# SESSION POLICIES IN AMAZON EKS POD IDENTITY

Amazon EKS Pod Identity has recently added session policies, allowing IAM permissions to be narrowed in a flexible and precise way for each pod without creating many separate IAM roles. This is an important improvement for applying the principle of least privilege more effectively in large Kubernetes environments.

Key points:

* A session policy is an inline IAM policy specified when creating or updating a Pod Identity association.
* Effective permissions are the intersection between the IAM role permissions and the session policy. In other words, a session policy can only reduce permissions, not expand them.
* This helps prevent over-permissioning when one IAM role is reused across workloads with different access requirements.
* It supports both same-account and cross-account scenarios through IAM role chaining.
* It reduces the number of IAM roles that need to be managed, which helps avoid IAM quota pressure in large clusters.
* It can be configured through the AWS Management Console, AWS CLI, or AWS SDK when creating an association between a Kubernetes ServiceAccount and an IAM role.

This feature is especially useful when many applications share the same IAM role but still need different access restrictions. For example, one pod may only need to read from a specific S3 bucket, while another only needs permission to call a limited set of APIs.

...Image...

...Link...

...Guide...
