---
title: "Foundation & Governance"
date: 2026-07-31
weight: 1
chapter: false
pre: "<b>1. </b>"
---

# Foundation & Governance

## 1. Mục tiêu

Thiết lập một môi trường AWS thống nhất cho toàn nhóm, kiểm soát chi phí phát sinh, và bảo đảm các thành viên triển khai tài nguyên theo cùng kiến trúc, region và quy ước quản lý.

## 2. Chuẩn hóa môi trường AWS

Nhóm thống nhất triển khai toàn bộ tài nguyên tại:

```text
ap-southeast-1 - Asia Pacific (Singapore)
```

![AWS region Singapore]({{< relURL "images/5-Workshop/5.3-DevOps/5.3-devops-aws-region-singapore.png" >}})

Các yêu cầu chung:

- Kiểm tra đúng AWS Account và region trước khi tạo resource.
- Không tự ý triển khai tài nguyên tại region khác.
- Báo lại tên resource, service và mục đích sử dụng sau khi tạo.
- Sử dụng cùng naming convention và tag convention.
- Dùng AWS CLI profile hoặc AWS Console đúng tài khoản được cấp.

## 3. Budget & Cost Monitoring

AWS Budgets được thiết lập để theo dõi đồng thời **chi phí phát sinh** và **mức sử dụng tài nguyên** trong quá trình triển khai dự án.

Hiện tại, nhóm sử dụng hai budget chính:

- `My Monthly Cost Budget`: theo dõi tổng chi phí AWS theo tháng, với hạn mức `100 USD`.
- `Daily usage`: theo dõi mức sử dụng của tài nguyên theo đơn vị giờ, với hạn mức `0.2 hour`.

Tại thời điểm kiểm tra, tổng chi phí phát sinh trong tháng vẫn ở mức thấp so với hạn mức đã thiết lập. Budget đang ở trạng thái `Healthy` và chưa có ngưỡng cảnh báo nào bị vượt qua.

![AWS budget overview]({{< relURL "images/5-Workshop/5.3-DevOps/5.3-devops-aws-budget-overview.png" >}})

### Các ngưỡng cảnh báo chi phí

Đối với budget `My Monthly Cost Budget`, hệ thống được cấu hình các ngưỡng cảnh báo sau:

```text
12.5%  -> Cảnh báo khi chi phí thực tế vượt 12.50 USD
25%    -> Cảnh báo khi chi phí thực tế vượt 25.00 USD
50%    -> Cảnh báo khi chi phí thực tế vượt 50.00 USD
85%    -> Cảnh báo khi chi phí thực tế vượt 85.00 USD
90%    -> Cảnh báo khi chi phí thực tế vượt 90.00 USD
100%   -> Cảnh báo khi chi phí thực tế vượt 100.00 USD
100%   -> Cảnh báo khi chi phí dự báo vượt 100.00 USD
```

Các ngưỡng này giúp nhóm phát hiện sớm việc sử dụng tài nguyên vượt kế hoạch và có biện pháp kiểm tra trước khi chi phí tăng cao.

![AWS budget alerts]({{< relURL "images/5-Workshop/5.3-DevOps/5.3-devops-aws-budget-alerts.png" >}})

### Quy ước kiểm soát nội bộ

Dựa trên các ngưỡng AWS Budgets, nhóm áp dụng quy trình kiểm soát như sau:

```text
Từ 12.5 USD -> Kiểm tra dịch vụ đang phát sinh chi phí
Từ 25 USD   -> Rà soát tài nguyên đang chạy và owner phụ trách
Từ 50 USD   -> Hạn chế tạo thêm tài nguyên không cần thiết
Từ 85 USD   -> Tạm dừng các tài nguyên thử nghiệm
Từ 90 USD   -> Chỉ duy trì tài nguyên cần thiết cho MVP
Từ 100 USD  -> Dừng và kiểm tra toàn bộ tài nguyên tính phí
```

### Các dịch vụ cần theo dõi sát

Những dịch vụ có khả năng phát sinh chi phí đáng kể gồm:

* Amazon EC2.
* SageMaker Processing và Training.
* SageMaker Endpoint.
* Amazon CloudWatch Logs.
* Data transfer.
* Các tài nguyên hoạt động liên tục hoặc tính phí theo thời gian.

Trước khi tạo tài nguyên có khả năng phát sinh chi phí, thành viên cần thông báo:

```text
Service:
Resource name:
Instance type hoặc cấu hình:
Mục đích:
Thời gian dự kiến chạy:
Owner:
```

## 4. Service Quotas

Bên cạnh budget, nhóm cần theo dõi Service Quotas để tránh bị chặn khi triển khai MVP, đặc biệt với các dịch vụ như SageMaker hoặc các tài nguyên cần quota theo instance type.

Việc kiểm tra quota sớm giúp nhóm:

- biết trước tài nguyên nào có thể tạo được,
- tránh phụ thuộc vào một demo live nếu quota chưa sẵn sàng,
- và chuẩn bị phương án dự phòng khi cần.

![SageMaker service quota]({{< relURL "images/5-Workshop/5.3-DevOps/5.3-devops-sagemaker-service-quota.png" >}})

## 5. Architecture, Naming & Tag Convention

Kiến trúc tổng thể được thống nhất theo luồng:

```text
Simulator
-> AWS IoT Core
-> IoT Rule
-> Kinesis Data Firehose
-> S3 Raw
-> Data Processing
-> S3 Processed
-> SageMaker
-> FastAPI
-> SNS
```

Naming convention được áp dụng:

```text
local-aqi-{environment}-{resource-purpose}
```

Ví dụ:

```text
local-aqi-dev-s3-raw
local-aqi-dev-s3-processed
local-aqi-dev-firehose-to-s3
local-aqi-dev-sagemaker-execution-role
```

Tag convention tối thiểu:

```text
Project=local-aqi
Environment=dev
Owner=<member-name>
ManagedBy=manual
CostCenter=student-project
```

![AWS resource tags]({{< relURL "images/5-Workshop/5.3-DevOps/5.3-devops-aws-resource-tags.png" >}})

