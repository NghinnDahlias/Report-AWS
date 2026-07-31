---
title: "Test the API and Alert Cycle"
weight: 4
chapter: false
pre: " <b> 5.7.4. </b> "
---

#### Test the backend from a client machine

Get the current EC2 public IPv4 address and define:

```bash
BASE_URL=http://<PUBLIC_IP>:8000
```

Test the health endpoint:

```bash
curl -i "$BASE_URL/health"
```

Open Swagger UI:

```text
http://<PUBLIC_IP>:8000/docs
```

#### Test the forecast API

Call:

```bash
curl -i "$BASE_URL/forecast/station-01"
```

When the SageMaker Endpoint and station data are configured correctly, the API should return:

- source timestamps,
- forecast timestamps,
- forecast horizon,
- predicted PM2.5 values,
- and AQI values.

If the endpoint or source data is not ready, the API should return HTTP `503` instead of generating fake forecast output.

#### Test subscription registration

Send a subscription request:

```bash
curl -i -X POST "$BASE_URL/subscribe/" \
  -H 'Content-Type: application/json' \
  -d '{
    "email": "APPROVED_TEST_EMAIL",
    "station_id": "station-01",
    "threshold_aqi": 150
  }'
```

Amazon SNS sends a confirmation email. Open that email and choose **Confirm subscription**.

Use only an approved test email address. Do not expose real personal email addresses in the repository, logs, or screenshots.

#### Test alert delivery

Send a PM2.5 value:

```bash
curl -i -X POST "$BASE_URL/alert/" \
  -H 'Content-Type: application/json' \
  -d '{
    "station_id": "station-01",
    "pm25": 55.4
  }'
```

The backend should:

1. convert PM2.5 to AQI,
2. find confirmed subscribers,
3. compare against the alert threshold,
4. apply the cooldown window,
5. and publish to Amazon SNS when the conditions are met.

#### Enable the scheduled forecast cycle

Enable the timer only after the SageMaker Endpoint, station data, and IAM permissions have all been verified.

```bash
cd /opt/local-aqi-backend

sudo install -m 0644 deploy/local-aqi-forecast-cycle.service \
  /etc/systemd/system/

sudo install -m 0644 deploy/local-aqi-forecast-cycle.timer \
  /etc/systemd/system/

sudo systemctl daemon-reload
sudo systemctl enable --now local-aqi-forecast-cycle.timer
```

Check the schedule:

```bash
sudo systemctl list-timers local-aqi-forecast-cycle.timer
sudo systemctl status local-aqi-forecast-cycle.timer --no-pager
```

Check the latest run:

```bash
sudo systemctl status local-aqi-forecast-cycle.service --no-pager
sudo journalctl -u local-aqi-forecast-cycle.service -n 100 --no-pager
```

#### Completion criteria

This step is complete when the team has:

- deployed the FastAPI backend on Amazon EC2,
- allowed the backend to access DynamoDB, SageMaker, and SNS through IAM role permissions,
- started the application with `systemd`,
- tested the health, forecast, subscribe, and alert APIs,
- and configured the scheduled forecast and alert cycle.

When the demo is finished, stop the EC2 instance and the SageMaker Endpoint to reduce cost.
