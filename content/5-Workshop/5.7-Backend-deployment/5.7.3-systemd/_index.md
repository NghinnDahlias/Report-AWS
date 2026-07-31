---
title: "Run the Backend with systemd"
weight: 3
chapter: false
pre: " <b> 5.7.3. </b> "
---

#### Review the service definition

The bootstrap script creates:

```text
/etc/systemd/system/local-aqi-backend.service
```

Inspect it:

```bash
sudo systemctl cat local-aqi-backend
```

Expected service configuration:

```ini
[Unit]
Description=Local AQI FastAPI backend
After=network-online.target
Wants=network-online.target

[Service]
Type=simple
User=ec2-user
Group=ec2-user
WorkingDirectory=/opt/local-aqi-backend
EnvironmentFile=-/opt/local-aqi-backend/.env
ExecStart=/opt/local-aqi-backend/.venv/bin/uvicorn app.main:app --host 0.0.0.0 --port 8000
Restart=always
RestartSec=5

[Install]
WantedBy=multi-user.target
```

#### Start the backend

Reload `systemd`:

```bash
sudo systemctl daemon-reload
```

Enable auto-start on boot:

```bash
sudo systemctl enable local-aqi-backend
```

Start the service:

```bash
sudo systemctl start local-aqi-backend
```

Check its status:

```bash
sudo systemctl status local-aqi-backend --no-pager
```

Expected result:

```text
Active: active (running)
```

#### Review logs

Show the latest 100 log lines:

```bash
sudo journalctl -u local-aqi-backend -n 100 --no-pager
```

Follow logs in real time:

```bash
sudo journalctl -u local-aqi-backend -f
```

Logs should not expose email addresses, credentials, access keys, or sensitive payloads.

#### Test the health endpoint locally

Call the API from inside the EC2 instance:

```bash
curl -i http://127.0.0.1:8000/health
```

Expected response:

```text
HTTP/1.1 200 OK
```

```json
{"status":"ok"}
```

If the API is not running correctly, review:

```bash
sudo systemctl status local-aqi-backend --no-pager
sudo journalctl -u local-aqi-backend -n 100 --no-pager
sudo ss -lntp | grep 8000
```
