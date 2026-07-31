---
title: "Install and Configure the Backend"
weight: 2
chapter: false
pre: " <b> 5.7.2. </b> "
---

#### Connect to the EC2 instance

1. Open **Amazon EC2**.
2. Select the instance `local-aqi-dev-ec2-backend`.
3. Choose **Connect**.
4. Open the **Session Manager** tab.
5. Choose **Connect**.

Check the Python version:

```bash
python3 --version
```

Install the required tools:

```bash
sudo dnf install -y python3-pip git rsync
```

#### Download the source code

Move to the EC2 user home directory:

```bash
cd /home/ec2-user
```

Clone the repository:

```bash
git clone <REPOSITORY_URL> AWS-FCJ-local_aqi_forecast
cd AWS-FCJ-local_aqi_forecast
```

Run the bootstrap script:

```bash
sudo bash backend/deploy/ec2-user-data.sh
```

Sync the backend source into `/opt/local-aqi-backend`:

```bash
sudo rsync -a --delete \
  --exclude '.env' \
  --exclude '.venv' \
  backend/ /opt/local-aqi-backend/

sudo chown -R ec2-user:ec2-user /opt/local-aqi-backend
```

#### Install dependencies

Move into the backend directory:

```bash
cd /opt/local-aqi-backend
```

Create the virtual environment:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

Install dependencies:

```bash
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

#### Configure environment variables

Create the `.env` file:

```bash
cp .env.example .env
chmod 600 .env
```

Edit it:

```bash
nano .env
```

Update the values:

```dotenv
AWS_REGION=ap-southeast-1
SUBSCRIBERS_TABLE=local-aqi-subscribers-dev
ALERTS_TOPIC_ARN=arn:aws:sns:ap-southeast-1:ACCOUNT_ID:local-aqi-alerts-dev

SAGEMAKER_ENDPOINT_NAME=ENDPOINT_NAME
SAGEMAKER_CONTENT_TYPE=application/json
SAGEMAKER_TIMEOUT_SECONDS=5
SAGEMAKER_MAX_ATTEMPTS=3
FORECAST_HORIZON_HOURS=24

STATION_DATA_FILE=/opt/local-aqi-backend/runtime/stations.json
ALLOW_SAMPLE_STATION_DATA=false
ALERT_COOLDOWN_SECONDS=3600
```

Replace `ACCOUNT_ID` and `ENDPOINT_NAME` with the actual values.

Do not store AWS access keys, secret keys, or personal email addresses in `.env`.

#### Validate the backend source

Run the test suite:

```bash
python -m unittest discover -s tests -v
```

Check syntax:

```bash
python -m compileall -q app tests
```

Validate the OpenAPI document:

```bash
python scripts/validate_openapi.py
```

If all commands succeed, continue to the `systemd` step.
