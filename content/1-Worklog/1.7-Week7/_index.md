---
title: "Week 7 Worklog"
date: 2026-07-18
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Week 7 Objectives:

* Run end-to-end integration tests for the full system.
* Evaluate valid data, invalid data, and service failure scenarios.
* Verify the alerting flow when PM2.5 exceeds the threshold.
* Use CloudWatch Logs Insights to isolate issues.
* Complete the testing report with supporting evidence.

### Tasks Completed This Week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 1 | Verify that valid telemetry data reaches S3 Raw | 13/07/2026 | 13/07/2026 | Internal test cases |
| 2 | Test invalid schema scenarios | 14/07/2026 | 14/07/2026 | Internal test cases |
| 3 | Test the Raw-to-Processed data flow | 15/07/2026 | 15/07/2026 | Team pipeline documentation |
| 4 | Test backend calls to the SageMaker Endpoint | 16/07/2026 | 16/07/2026 | API tests |
| 5 | Test both normal forecast cases and sudden PM2.5 spike scenarios | 17/07/2026 | 17/07/2026 | Test scenarios |
| 6 | Test endpoint unavailability and query errors with CloudWatch Logs Insights | 18/07/2026 | 18/07/2026 | CloudWatch Logs Insights |
| 6 | Compile screenshots, API responses, alert emails, and logs into the testing report | 18/07/2026 | 18/07/2026 | Test Report |

### Outcomes This Week:

* Confirmed that the ingestion flow works correctly with valid telemetry.
* Ensured the system logs or handles invalid schema inputs instead of breaking the pipeline.
* Verified that data is processed and stored in the correct locations from Raw to Processed.
* Confirmed that the API receives real forecast results from the SageMaker Endpoint.
* Verified that the system does not send false alerts in normal conditions.
* Confirmed that Amazon SNS sends warning emails successfully when PM2.5 exceeds the threshold.
* Verified that the backend handles timeout or service failure scenarios appropriately when the endpoint is unavailable.
* Identified faulty modules using CloudWatch Logs Insights.
* Completed an end-to-end testing report with clear supporting evidence.
