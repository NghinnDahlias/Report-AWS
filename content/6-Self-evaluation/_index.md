---
title: "Self-Assessment"
date: 2026-07-31
weight: 6
chapter: false
pre: " <b> 6. </b> "
---

{{% notice warning %}}
**Note:** The content below is provided for reference only. Please do not copy it verbatim into your final report.
{{% /notice %}}

After eight weeks in the **AWS First Cloud AI Journey** program, with the role of **DevOps/QA & Documentation** in the team implementing **Topic 5 - Machine Learning on AWS**, I had the opportunity to apply what I learned in school to the process of building and operating a real machine learning system on AWS.

During the internship, I participated in managing the team's AWS environment, setting up access control, monitoring costs, supporting backend deployment, observing the system, validating integration flows, organizing project documentation, and preparing demo materials. Through that process, I gained a clearer understanding of the relationship between cloud infrastructure, data pipelines, machine learning models, backend services, and real operational workflows.

## 1. Knowledge, skills, and outcomes gained

### Professional knowledge

Through the project, I gained and reinforced the following knowledge:

* Understanding the end-to-end architecture of a machine learning system on AWS, including the flow from **AWS IoT Core**, **Amazon Data Firehose**, **Amazon S3**, **Amazon SageMaker Processing**, **SageMaker Endpoint**, **FastAPI**, to **Amazon SNS**.
* Understanding how to organize and manage AWS accounts securely using **root account protection**, **MFA**, **IAM User**, **IAM Group**, **IAM Role**, and the **least privilege** principle.
* Understanding the role of IAM service roles in allowing AWS services to interact securely without storing access keys in source code.
* Understanding how to deploy a backend service on Amazon EC2, configure security groups, and use IAM instance roles.
* Understanding how to use Amazon CloudWatch for log collection, metric monitoring, dashboard creation, and troubleshooting with CloudWatch Logs Insights.
* Understanding the process of integration testing and end-to-end validation for a system with multiple connected components.
* Understanding the importance of resource inventory, naming conventions, tagging, log retention, AWS Budgets, and cleanup practices in managing cloud resources and costs.
* Gaining practical experience in choosing, configuring, and operating AWS resources based on technical requirements, security constraints, and project budget.

### Skills developed

During the internship, I improved the following skills:

* Managing IAM users, IAM groups, IAM roles, and IAM policies on AWS.
* Configuring Amazon EC2, security groups, and IAM instance profiles.
* Setting up AWS Budgets and monitoring cloud cost usage.
* Using CloudWatch Logs, CloudWatch Metrics, CloudWatch Dashboards, and Logs Insights.
* Performing integration testing and end-to-end validation across multiple modules.
* Analyzing logs to identify the location and root cause of failures.
* Creating test cases for valid data, invalid data, service failures, and alert-threshold scenarios.
* Managing resources using naming conventions, tag conventions, and a resource inventory.
* Writing technical documentation such as README files, runbooks, architecture notes, test reports, and cost/cleanup documents.
* Collaborating with teammates responsible for Ingestion, Data, Machine Learning, and Backend.
* Consolidating documents, demo content, and presentation flow for the team.
* Reporting progress and discussing technical issues clearly with other team members.

### Deliverables contributed

The deliverables I contributed to include:

* The IAM and access-control foundation for the team AWS account.
* AWS Budgets and cost-monitoring guardrails for the project.
* Naming convention and tag convention guidelines for AWS resources.
* A resource inventory used to track ownership, status, and cleanup requirements.
* The EC2 environment for FastAPI deployment used in testing and demo activities.
* CloudWatch log groups, Logs Insights queries, and monitoring dashboards.
* End-to-end test cases and validation evidence.
* Project documents including architecture notes, contracts, runbooks, deployment guides, and cleanup instructions.
* Demo scripts, screenshots, and backup materials.
* Cost review notes and evidence of AWS resource cleanup after the demo.

## 2. Personal reflection

The **AWS First Cloud AI Journey** program was organized in a structured way and provided practical materials and lab activities that helped students approach cloud services through hands-on work. Whenever I faced technical issues or uncertainty about the right implementation direction, I received support from mentors and teammates, which helped me continue and complete the assigned tasks.

The biggest difference compared with classroom learning was that I had to directly manage and operate resources in a real AWS account. Every IAM configuration, EC2 instance, SageMaker endpoint, or CloudWatch log group could affect security, availability, and cost for the whole project. Because of that, I not only learned how to create resources, but also how to think about permissions, monitoring, failure handling, and cleanup after use.

One of the hardest parts for me was designing suitable IAM permissions for different members and services. If permissions were too limited, the team could not finish tasks. If permissions were too broad, the account could face security risks or uncontrolled resource creation. To handle that, I analyzed service interactions, identified the minimum required permissions, and created separate IAM roles for specific purposes.

Another challenge was end-to-end testing across components owned by different teammates. A problem detected at the backend layer did not always originate there; it could come from the input data, Firehose, processing jobs, S3 permissions, or the SageMaker endpoint. Setting up CloudWatch logs and keeping logs consistent across modules helped me narrow down where issues happened instead of checking the whole system manually.

The most important lesson I learned is that DevOps is not only about launching a server or configuring an AWS account. It also includes building a safe working environment for the team, monitoring system behavior, controlling cost, handling incidents, validating integration, and ensuring resources are cleaned up after project completion.

Through the **DevOps/QA & Documentation** role, I had the chance to observe the system as a whole rather than focusing on only one module. That helped me build a stronger systems-thinking mindset and understand how infrastructure, data, machine learning, backend services, and operations connect in a real cloud project.

## 3. Self-rating

To reflect objectively on my internship process, I assess myself using the following criteria:

| No. | Criteria | Description | Good | Fair | Average |
| --- | --- | --- | --- | --- | --- |
| 1 | **Professional knowledge and skills** | Understanding the system architecture, using AWS tools, and applying knowledge in practice | x |  |  |
| 2 | **Learning ability** | Absorbing new knowledge and exploring AWS services that I had not used before | x |  |  |
| 3 | **Proactiveness** | Looking up documentation, proposing approaches, and handling tasks without waiting passively | x |  |  |
| 4 | **Sense of responsibility** | Tracking assigned work, supporting the team, and trying to complete tasks on time | x |  |  |
| 5 | **Discipline** | Following schedule, rules, and work planning |  | x |  |
| 6 | **Willingness to improve** | Accepting feedback, fixing mistakes, and improving work quality | x |  |  |
| 7 | **Communication** | Presenting ideas, reporting progress, and discussing technical issues with teammates |  | x |  |
| 8 | **Teamwork** | Working with members across Ingestion, Data, ML, and Backend | x |  |  |
| 9 | **Professional attitude** | Respecting mentors, teammates, and maintaining a serious working attitude | x |  |  |
| 10 | **Problem-solving mindset** | Analyzing issues, finding root causes, and proposing suitable fixes |  | x |  |
| 11 | **Contribution to the project** | Participating in infrastructure management, testing, monitoring, documentation, and demo preparation | x |  |  |
| 12 | **Overall evaluation** | General performance in the DevOps/QA & Documentation role | x |  |  |

## 4. Areas for improvement

Besides the knowledge and skills I gained, I believe I still need to improve in the following areas:

* Strengthening discipline, time management, and strict compliance with organizational rules.
* Improving planning ability and task prioritization.
* Developing a more systematic root-cause analysis mindset instead of focusing only on visible symptoms.
* Improving communication so that technical issues can be explained more briefly, clearly, and with the right emphasis.
* Reporting blockers earlier to avoid affecting the team's shared progress.
* Continuing to deepen my knowledge of AWS, DevOps, cloud security, monitoring, and deployment automation.
* Practicing better coordination when there are different viewpoints among team members.

## 5. Conclusion

The internship in the **AWS First Cloud AI Journey** program gave me valuable practical experience in deploying and operating a machine learning system on AWS. Beyond professional knowledge, I also strengthened my teamwork, system testing, resource management, technical writing, and issue-handling skills during project execution.

The knowledge, skills, and experience I gained during this internship form an important foundation for my continued learning and future development in Cloud Computing, DevOps, and Machine Learning.
