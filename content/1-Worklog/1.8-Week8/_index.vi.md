---
title: "Nhật ký công việc tuần 8"
date: 2026-07-25
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Mục tiêu tuần 8:

* Hoàn thiện bộ tài liệu cuối cùng của dự án.
* Tổng duyệt demo và chuẩn bị phương án dự phòng.
* Rà soát tài nguyên AWS có khả năng phát sinh chi phí cao.
* Cleanup các tài nguyên không còn sử dụng sau demo.
* Cập nhật trạng thái cuối cùng vào Resource Inventory.

### Các công việc thực hiện trong tuần:

| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 1 | Hoàn thiện README và tài liệu triển khai | 20/07/2026 | 20/07/2026 | README, Runbook |
| 2 | Hoàn thiện Architecture Diagram, Data Contract, API Contract và Inference Contract | 21/07/2026 | 21/07/2026 | Tài liệu thiết kế hệ thống |
| 3 | Hoàn thiện Test Report và Resource Inventory | 22/07/2026 | 22/07/2026 | Test Report, Resource Inventory |
| 4 | Chuẩn bị kịch bản demo cho luồng bình thường và kịch bản ô nhiễm tăng đột biến | 23/07/2026 | 23/07/2026 | Demo script |
| 5 | Điều phối demo rehearsal và chuẩn bị ảnh chụp, video dự phòng | 24/07/2026 | 24/07/2026 | Tài liệu demo |
| 6 | Xóa SageMaker Endpoint khi không sử dụng, stop hoặc terminate EC2 phù hợp | 25/07/2026 | 25/07/2026 | AWS Console |
| 6 | Kiểm tra Elastic IP, NAT Gateway, CloudWatch Log Group, AWS Billing và cập nhật Resource Inventory | 25/07/2026 | 25/07/2026 | AWS Billing Dashboard |

### Kết quả đạt được trong tuần:

* Có hướng dẫn tổng thể để cài đặt, vận hành và kiểm thử hệ thống.
* Kiến trúc và ranh giới giữa các module được mô tả rõ ràng.
* Có bằng chứng kiểm thử và danh sách tài nguyên đầy đủ.
* Có kịch bản demo cho cả luồng bình thường và tình huống ô nhiễm tăng đột biến.
* Các thành viên nắm rõ phần trình bày và trình tự demo.
* Giảm rủi ro khi kết nối hoặc dịch vụ AWS gặp sự cố nhờ tài liệu và tư liệu dự phòng.
* Hạn chế chi phí inference phát sinh sau demo bằng việc xóa SageMaker Endpoint khi không sử dụng.
* Không để EC2 hoặc các tài nguyên đắt đỏ tiếp tục phát sinh chi phí ngoài kế hoạch.
* Hoàn thành quá trình cleanup và cập nhật trạng thái cuối cùng của tài nguyên AWS.
