---
title: "Nhật ký công việc tuần 6"
date: 2026-07-11
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6:

* Hỗ trợ triển khai model candidate thành SageMaker Endpoint.
* Kiểm tra quyền truy cập và logging của SageMaker.
* Triển khai môi trường chạy FastAPI trên Amazon EC2.
* Cấu hình Security Group và IAM Instance Role an toàn.
* Viết hướng dẫn vận hành để tối ưu chi phí sử dụng tài nguyên.

### Các công việc thực hiện trong tuần:

| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 1 | Hỗ trợ kiểm tra SageMaker Execution Role và quyền truy cập model artifact trên S3 | 06/07/2026 | 06/07/2026 | Amazon SageMaker |
| 2 | Hỗ trợ triển khai và kiểm tra SageMaker Endpoint | 07/07/2026 | 07/07/2026 | Amazon SageMaker Endpoint |
| 3 | Kiểm tra CloudWatch metrics của endpoint như invocation, độ trễ và lỗi inference | 08/07/2026 | 08/07/2026 | CloudWatch Metrics |
| 4 | Tạo và cấu hình EC2 cho Backend chạy FastAPI | 09/07/2026 | 09/07/2026 | Amazon EC2 |
| 5 | Cấu hình Security Group theo hướng chỉ mở các cổng cần thiết | 10/07/2026 | 10/07/2026 | EC2 Security Group |
| 6 | Gắn IAM Instance Role cho EC2 và kiểm tra Backend gọi SageMaker Endpoint, Amazon SNS | 11/07/2026 | 11/07/2026 | IAM Instance Profile |
| 6 | Viết hướng dẫn start/stop EC2 và endpoint để hỗ trợ vận hành và cleanup | 11/07/2026 | 11/07/2026 | Runbook nội bộ |

### Kết quả đạt được trong tuần:

* Endpoint có đủ quyền đọc model artifact và ghi log.
* Endpoint chuyển sang trạng thái `InService` và có thể nhận request.
* Theo dõi được invocation, độ trễ và lỗi inference trên CloudWatch.
* Có môi trường AWS để chạy FastAPI phục vụ demo.
* Chỉ mở các cổng cần thiết, hạn chế truy cập không phù hợp.
* Backend gọi được dịch vụ AWS mà không cần lưu access key trong source code.
* Có quy trình vận hành và cleanup nhằm hạn chế chi phí.
