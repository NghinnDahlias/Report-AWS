---
title: "Monitoring & Quality Assurance"
date: 2026-07-31
weight: 3
chapter: false
pre: "<b>3. </b>"
---

# Monitoring & Quality Assurance

## 1. Mục tiêu

Theo dõi trạng thái hoạt động của các service, thu thập log cần thiết và kiểm thử toàn bộ luồng trước khi nghiệm thu.

## 2. Monitoring & Logging

Các thành phần cần theo dõi:

- AWS IoT Core và IoT Rule.
- Amazon Data Firehose.
- Amazon S3 Raw và Processed.
- SageMaker Processing hoặc Training Job.
- Backend API.
- Amazon SNS.

Thông tin cần kiểm tra:

```text
Incoming records
Delivery success
Delivery failure
Data freshness
Training job status
API error
SNS publish result
```

Khi báo lỗi, thành viên phải cung cấp:

```text
Timestamp:
Resource name:
Error message:
Log location:
Action đang thực hiện:
```

![CloudWatch log events]({{< relURL "images/5-Workshop/5.3-DevOps/5.3-3-cloudwatch-log-events.png" >}})

## 3. Kiểm thử từng module

### Ingestion

- Một message.
- Nhiều message.
- Nhiều station.
- Payload thiếu field.
- Publish lỗi.

### Data

- Đọc JSON từ S3 Raw.
- Xử lý concatenated JSON.
- Kiểm tra null.
- Kiểm tra duplicate.
- Kiểm tra giá trị âm.
- Kiểm tra timestamp UTC.
- Ghi và đọc lại Parquet.

### Machine Learning

- Đọc dataset processed.
- Chạy training.
- Kiểm tra model artifact.
- Tạo forecast 24 giờ.
- Ghi nhận MAE/RMSE.
- Kiểm tra trạng thái Training Job.

### Backend

- Health check.
- Forecast station hợp lệ.
- Station không tồn tại.
- Endpoint chưa sẵn sàng.
- SNS publish thành công.
- Email subscription đã confirmed.

## 4. Integration Testing

Luồng nghiệm thu:

```text
Simulator
→ AWS IoT Core
→ IoT Rule
→ Firehose
→ S3 Raw
→ Data Processing
→ S3 Processed
→ ML Forecast
→ Backend
→ SNS Email
```

### Kịch bản bình thường

- Nhiều station gửi dữ liệu.
- IoT Core nhận message.
- Firehose ghi S3 Raw.
- Pipeline tạo processed data.
- ML tạo forecast.
- Backend trả kết quả.

### Kịch bản vượt ngưỡng

- PM2.5 tăng cao.
- Backend kích hoạt SNS.
- Người dùng nhận email.

### Kịch bản lỗi

- Payload thiếu field.
- PM2.5 sai kiểu dữ liệu.
- Duplicate.
- Station ID không hợp lệ.
- API nhận station không tồn tại.

![Ingestion evidence]({{< relURL "images/5-Workshop/5.3-DevOps/5.3-3-ingestion-evidence.png" >}})

## 5. Biểu mẫu kết quả

```text
Test case:
Input:
Expected result:
Actual result:
Status: Pass / Fail
Evidence:
Owner:
```

## 6. Tiêu chí nghiệm thu

- Simulator gửi được dữ liệu.
- IoT Core nhận message.
- Firehose ghi được S3 Raw.
- Processed data đọc được bằng Parquet.
- ML tạo được forecast.
- Backend trả đúng response.
- SNS gửi email khi vượt ngưỡng.
- Có log và evidence cho các bước chính.

## 7. Kết quả đạt được

- Có test case cho từng module.
- Có quy trình báo lỗi thống nhất.
- Có evidence kiểm thử integration.
- Lỗi có thể được xác định theo từng chặng.

