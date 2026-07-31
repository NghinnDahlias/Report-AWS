---
title: "Blogs Posted"
date: 2026-31-07
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

{{% notice warning %}}
⚠️ **Note:** The information below is for reference purposes only. Please **do not copy it verbatim** into your report.
{{% /notice %}}

This section lists the blogs posted during the internship and summarizes the main technical idea of each article.

### [Blog 1 - Why does an IAM role with AWS service permissions still not work?](3.1-Blog1/)

This blog explains why an IAM role can appear to have the correct permissions and still fail when used by an AWS service. It focuses on the relationship between **Trust Policy**, **Permission Policy**, and the user's `iam:PassRole` permission when configuring AWS resources.

### [Blog 2 - Why is REST API not always the best choice? The power of Pub/Sub and MQTT in distributed systems](3.2-Blog2/)

This blog compares the traditional synchronous HTTP/REST model with the Publish/Subscribe approach, especially in systems that process real-time telemetry from many devices. It highlights why **Pub/Sub** and **MQTT** are often better suited for event-driven, loosely coupled architectures.

### [Blog 3 - Session policies in Amazon EKS Pod Identity](3.3-Blog3/)

This blog introduces the **session policies** feature in Amazon EKS Pod Identity, showing how IAM permissions can be narrowed per pod without creating many separate IAM roles. It emphasizes the principle of least privilege and why this feature is useful in large Kubernetes environments.
