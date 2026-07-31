---
title: "Workshop"
date: 2026-07-31
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

{{% notice info %}}
Phần này là **dự án kỹ thuật chính** của báo cáo. Nội dung được tổ chức theo vai trò trong nhóm để bám sát cả cách triển khai thực tế lẫn luồng demo end-to-end cuối cùng.
{{% /notice %}}

# Workshop triển khai Local AQI Forecasting & Alert System trên AWS

#### Tổng quan

Workshop này được viết theo **một luồng end-to-end hoàn chỉnh** thay vì tách rời từng dịch vụ AWS riêng lẻ. Mỗi vai trò sẽ trình bày:

+ đã triển khai những bước nào,
+ đã tạo ra thành phần nào,
+ và đạt được kết quả gì trong toàn bộ hệ thống.

Luồng demo chính:

```text
Simulator
-> AWS IoT Core
-> IoT Rule
-> Kinesis Data Firehose
-> S3 Raw
-> Data Processing
-> S3 Processed
-> SageMaker Training / Forecast Result
-> FastAPI
-> SNS Email
```

#### Phân rã theo vai trò

+ `5.3 DevOps`: xác định bài toán, kiến trúc, naming/tagging, thiết lập tài khoản IAM và kiểm soát truy cập.
+ `5.4 Ingestion`: gửi dữ liệu từ simulator qua IoT Core, Firehose và vào S3 Raw.
+ `5.5 Data Preparation`: đọc dữ liệu raw, làm sạch và tạo dataset sẵn sàng cho Machine Learning.
+ `5.6 Machine Learning`: huấn luyện mô hình dự báo PM2.5 và tạo kết quả forecast.
+ `5.7 Backend`: cung cấp API và gửi cảnh báo qua SNS.

#### Nội dung

1. [Giới thiệu workshop](5.1-Workshop-overview/)
2. [Điều kiện chuẩn bị](5.2-Prerequiste/)
3. [DevOps: kiến trúc, IAM và quản trị tài khoản](5.3-DevOps/)
4. [Ingestion: Simulator -> IoT Core -> Firehose -> S3 Raw](5.4-Ingestion/)
5. [Data Preparation: xử lý và chuẩn hóa dữ liệu](5.5-Data%20Preprocessing/)
6. [Machine Learning: huấn luyện và sinh kết quả dự báo](5.6-Machine%20learning/)
7. [Triển khai FastAPI backend](5.7-Backend-deployment/)
