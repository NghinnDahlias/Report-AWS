---
title: "Các bài blog đã đăng"
date: 2026-08-01
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}

Phần này tổng hợp các bài blog đã đăng trong thời gian thực tập và tóm tắt ngắn ý chính của từng bài viết.

### [Blog 1 - IAM Role có quyền nhưng AWS service vẫn không dùng được?](3.1-Blog1/)

Bài viết này giải thích vì sao một IAM Role nhìn như đã có đủ permission nhưng AWS service vẫn không thể sử dụng. Trọng tâm của bài là mối quan hệ giữa **Trust Policy**, **Permission Policy** và quyền `iam:PassRole` của người đang cấu hình tài nguyên AWS.

### [Blog 2 - Vì sao REST API không phải lúc nào cũng là lựa chọn tốt nhất? Sức mạnh của Pub/Sub và MQTT trong distributed systems](3.2-Blog2/)

Bài viết này so sánh mô hình HTTP/REST đồng bộ truyền thống với mô hình Publish/Subscribe trong các hệ thống xử lý telemetry thời gian thực. Nội dung làm rõ vì sao **Pub/Sub** và **MQTT** thường phù hợp hơn với kiến trúc event-driven và các thành phần cần giao tiếp lỏng kết.

### [Blog 3 - Session Policies trong Amazon EKS Pod Identity](3.3-Blog3/)

Bài viết này giới thiệu tính năng **session policies** trong Amazon EKS Pod Identity, cho phép thu hẹp quyền IAM theo từng pod mà không cần tạo quá nhiều IAM Role riêng biệt. Đây là một cải tiến hữu ích để áp dụng nguyên tắc least privilege hiệu quả hơn trong môi trường Kubernetes lớn.
