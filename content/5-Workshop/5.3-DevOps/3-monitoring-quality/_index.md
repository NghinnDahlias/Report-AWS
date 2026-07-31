---
title: "Monitoring & Quality Assurance"
date: 2026-07-31
weight: 3
chapter: false
pre: "<b>3. </b>"
---

# Monitoring & Quality Assurance

## 1. Objective

Monitor service health, collect essential logs, and validate the end-to-end flow before final acceptance.

## 2. Monitoring & Logging

The main components to monitor include:

- AWS IoT Core and IoT Rule.
- Amazon Data Firehose.
- Amazon S3 Raw and Processed.
- SageMaker Processing or Training Jobs.
- Backend API.
- Amazon SNS.

The team should verify:

```text
Incoming records
Delivery success
Delivery failure
Data freshness
Training job status
API error
SNS publish result
```

When reporting an issue, each member should provide:

```text
Timestamp:
Resource name:
Error message:
Log location:
Action in progress:
```

![CloudWatch log events]({{< relURL "images/5-Workshop/5.3-DevOps/5.3-3-cloudwatch-log-events.png" >}})

## 3. Module-Level Testing

### Ingestion

- Single message.
- Multiple messages.
- Multiple stations.
- Missing-field payload.
- Publish failure.

### Data

- Read JSON from S3 Raw.
- Handle concatenated JSON.
- Check null values.
- Check duplicates.
- Check negative values.
- Check UTC timestamps.
- Write and read Parquet again.

### Machine Learning

- Read the processed dataset.
- Run training.
- Check the model artifact.
- Generate a 24-hour forecast.
- Record MAE/RMSE.
- Check the Training Job status.

### Backend

- Health check.
- Valid station forecast request.
- Non-existent station.
- Endpoint not ready.
- Successful SNS publish.
- Confirmed email subscription.

## 4. Integration Testing

Acceptance flow:

```text
Simulator
-> AWS IoT Core
-> IoT Rule
-> Firehose
-> S3 Raw
-> Data Processing
-> S3 Processed
-> ML Forecast
-> Backend
-> SNS Email
```

### Normal scenario

- Multiple stations send data.
- IoT Core receives messages.
- Firehose writes to S3 Raw.
- The pipeline produces processed data.
- ML generates forecasts.
- The backend returns results.

### Threshold-exceeded scenario

- PM2.5 rises above the alert threshold.
- The backend triggers SNS.
- The user receives an email alert.

### Failure scenario

- Payload missing required fields.
- PM2.5 has the wrong data type.
- Duplicate records appear.
- Station ID is invalid.
- The API receives a non-existent station.

![Ingestion evidence]({{< relURL "images/5-Workshop/5.3-DevOps/5.3-3-ingestion-evidence.png" >}})

## 5. Result Template

```text
Test case:
Input:
Expected result:
Actual result:
Status: Pass / Fail
Evidence:
Owner:
```

## 6. Acceptance Criteria

- The simulator can send data.
- IoT Core receives messages.
- Firehose writes to S3 Raw.
- Processed data can be read in Parquet format.
- ML can generate forecasts.
- The backend returns the correct response.
- SNS sends email when thresholds are exceeded.
- Logs and evidence exist for each major step.

## 7. Outcomes Achieved

- Test cases exist for each module.
- A consistent issue-reporting process is defined.
- Integration evidence is collected.
- Failures can be isolated by stage.

