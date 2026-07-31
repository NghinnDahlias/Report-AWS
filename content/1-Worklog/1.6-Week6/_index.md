---
title: "Week 6 Worklog"
date: 2026-07-11
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Week 6 Objectives:

* Support the deployment of the model candidate as a SageMaker Endpoint.
* Verify SageMaker permissions and logging behavior.
* Deploy the FastAPI runtime environment on Amazon EC2.
* Configure Security Groups and IAM Instance Roles securely.
* Write operating instructions to optimize resource costs.

### Tasks Completed This Week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 1 | Support the review of the SageMaker Execution Role and access to model artifacts in S3 | 06/07/2026 | 06/07/2026 | Amazon SageMaker |
| 2 | Support deployment and validation of the SageMaker Endpoint | 07/07/2026 | 07/07/2026 | Amazon SageMaker Endpoint |
| 3 | Check CloudWatch metrics for the endpoint, including invocations, latency, and inference errors | 08/07/2026 | 08/07/2026 | CloudWatch Metrics |
| 4 | Create and configure EC2 for running the FastAPI backend | 09/07/2026 | 09/07/2026 | Amazon EC2 |
| 5 | Configure Security Groups to open only the required ports | 10/07/2026 | 10/07/2026 | EC2 Security Group |
| 6 | Attach an IAM Instance Role to EC2 and validate backend calls to SageMaker Endpoint and Amazon SNS | 11/07/2026 | 11/07/2026 | IAM Instance Profile |
| 6 | Write start/stop instructions for EC2 and the endpoint to support operations and cleanup | 11/07/2026 | 11/07/2026 | Internal runbook |

### Outcomes This Week:

* Ensured the endpoint had permission to read model artifacts and write logs.
* Brought the endpoint into `InService` state and made it ready to receive requests.
* Monitored invocations, latency, and inference errors through CloudWatch.
* Prepared an AWS environment for running FastAPI during the demo.
* Limited exposure by opening only necessary ports.
* Enabled the backend to call AWS services without storing access keys in source code.
* Established an operating and cleanup process to reduce unnecessary costs.
