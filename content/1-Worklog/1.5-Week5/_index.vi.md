---
title: "Nhật ký công việc tuần 5"
date: 2026-07-04
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu tuần 5:

* Hỗ trợ triển khai các dịch vụ AWS đầu tiên của hệ thống.
* Xây dựng IAM Role phù hợp cho các dịch vụ tương tác với nhau.
* Thiết lập khả năng quan sát hệ thống bằng Amazon CloudWatch.
* Kiểm tra log ở các thành phần ingestion, processing và backend.
* Quản lý log retention để tránh phát sinh chi phí không cần thiết.

### Các công việc thực hiện trong tuần:

| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 1 | Hỗ trợ tạo IAM Role cho AWS IoT Core, Firehose và các dịch vụ liên quan | 29/06/2026 | 29/06/2026 | AWS IAM Role |
| 2 | Kiểm tra log của luồng IoT/Ingestion và Firehose | 30/06/2026 | 30/06/2026 | Amazon CloudWatch |
| 3 | Thiết lập log cho Processing và Backend | 01/07/2026 | 01/07/2026 | CloudWatch Logs |
| 4 | Tìm hiểu và thực hành CloudWatch Logs Insights để truy vấn lỗi | 02/07/2026 | 02/07/2026 | CloudWatch Logs Insights |
| 5 | Xây dựng CloudWatch Dashboard cơ bản để theo dõi log và metric chính | 03/07/2026 | 03/07/2026 | CloudWatch Dashboard |
| 6 | Thiết lập log retention phù hợp cho các log group | 04/07/2026 | 04/07/2026 | CloudWatch Log Retention |

### Kết quả đạt được trong tuần:

* Các dịch vụ có thể tương tác với nhau mà không cần hard-code access key.
* Có dữ liệu log phục vụ việc xác định lỗi trong pipeline đầu vào.
* Có thể theo dõi quá trình xử lý dữ liệu và hoạt động của API.
* Biết cách truy vấn và lọc các sự kiện lỗi bằng Logs Insights.
* Có giao diện tập trung để theo dõi log và metric chính.
* Hạn chế chi phí phát sinh do lưu log không giới hạn.
