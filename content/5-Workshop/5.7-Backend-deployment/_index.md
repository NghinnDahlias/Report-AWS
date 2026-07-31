---
title: "FastAPI Backend Deployment"
date: 2026-07-31
weight: 7
chapter: false
pre: " <b> 5.7. </b> "
---

#### Overview

In this section, you will deploy the backend of the **Local AQI Forecasting & Alert System** to Amazon EC2.

The backend is built with FastAPI and is responsible for:

- providing API endpoints to check system health,
- receiving AQI alert-threshold subscription requests,
- storing subscription data and cooldown status in Amazon DynamoDB,
- calling the SageMaker Endpoint to retrieve forecast results,
- and sending alert emails through Amazon SNS.

Backend flow:

```text
User
    -> FastAPI on Amazon EC2
        -> Amazon DynamoDB
        -> Amazon SageMaker Endpoint
        -> Amazon SNS
```

The backend uses the EC2 IAM role to access AWS services. The application is managed with `systemd` so it can restart automatically when EC2 starts or when the process fails.

#### Content

- [Prepare EC2 and IAM role](5.7.1-prepare/)
- [Install and configure the backend](5.7.2-install/)
- [Run the backend with systemd](5.7.3-systemd/)
- [Test the API and alert cycle](5.7.4-test/)
