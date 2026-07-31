---
title: "Nhật ký công việc tuần 7"
date: 2026-07-18
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu tuần 7:

* Kiểm thử tích hợp toàn bộ hệ thống end-to-end.
* Đánh giá các trường hợp dữ liệu hợp lệ, dữ liệu lỗi và lỗi dịch vụ.
* Xác minh luồng cảnh báo khi PM2.5 vượt ngưỡng.
* Sử dụng CloudWatch Logs Insights để khoanh vùng sự cố.
* Hoàn thiện báo cáo kiểm thử với đầy đủ bằng chứng.

### Các công việc thực hiện trong tuần:

| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 1 | Kiểm tra telemetry hợp lệ đi vào S3 Raw | 13/07/2026 | 13/07/2026 | Test case nội bộ |
| 2 | Kiểm tra trường hợp dữ liệu sai schema | 14/07/2026 | 14/07/2026 | Test case nội bộ |
| 3 | Kiểm tra luồng Raw sang Processed | 15/07/2026 | 15/07/2026 | Pipeline tài liệu nhóm |
| 4 | Kiểm tra Backend gọi SageMaker Endpoint | 16/07/2026 | 16/07/2026 | API test |
| 5 | Kiểm tra trường hợp forecast bình thường và trường hợp PM2.5 tăng đột biến | 17/07/2026 | 17/07/2026 | Kịch bản kiểm thử |
| 6 | Kiểm tra trường hợp endpoint không khả dụng và truy vấn lỗi bằng CloudWatch Logs Insights | 18/07/2026 | 18/07/2026 | CloudWatch Logs Insights |
| 6 | Tổng hợp ảnh chụp màn hình, response API, email cảnh báo và log vào báo cáo kiểm thử | 18/07/2026 | 18/07/2026 | Test Report |

### Kết quả đạt được trong tuần:

* Xác nhận luồng Ingestion hoạt động đúng với telemetry hợp lệ.
* Hệ thống xử lý hoặc ghi log lỗi khi dữ liệu sai schema thay vì làm hỏng pipeline.
* Dữ liệu được xử lý và lưu đúng vị trí trong luồng Raw sang Processed.
* API nhận được kết quả forecast thực tế từ SageMaker Endpoint.
* Hệ thống không gửi cảnh báo sai trong trường hợp bình thường.
* Amazon SNS gửi email cảnh báo thành công khi PM2.5 vượt ngưỡng.
* Backend xử lý timeout hoặc lỗi dịch vụ phù hợp khi endpoint không khả dụng.
* Xác định được module phát sinh lỗi bằng CloudWatch Logs Insights.
* Có báo cáo kiểm thử end-to-end kèm bằng chứng rõ ràng.
