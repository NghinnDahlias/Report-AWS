---
title: "Blog 3"
date: 2026-07-25
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}


# TĂNG MEMORY CHO AWS LAMBDA CÓ THỂ GIÚP GIẢM CHI PHÍ – TẠI SAO?

Khi cấu hình AWS Lambda, một suy nghĩ thường gặp là chọn mức memory thấp nhất để tiết kiệm chi phí. Cách suy luận này có vẻ hợp lý vì memory càng cao thì mức giá compute cho mỗi đơn vị thời gian càng lớn.

Tuy nhiên, memory của Lambda không chỉ quyết định lượng RAM. Khi tăng memory, AWS cũng phân bổ thêm CPU và một số tài nguyên xử lý khác cho function.

Do đó, một function có memory cao hơn có thể hoàn thành công việc nhanh hơn. Nếu thời gian chạy giảm đủ nhiều, tổng lượng GB-second và chi phí compute có thể thấp hơn cấu hình memory nhỏ.

## 1. Memory của Lambda không chỉ là RAM

AWS Lambda cho phép cấu hình memory từ 128 MB đến 10.240 MB với bước tăng 1 MB.

Khi tăng memory, function đồng thời nhận thêm:

* RAM.
* CPU.
* Khả năng xử lý.
* Tài nguyên hỗ trợ một số tác vụ mạng và I/O.

Ở mức 1.769 MB, Lambda cung cấp tài nguyên CPU tương đương khoảng một vCPU. Khi memory tiếp tục tăng, function có thể nhận thêm tài nguyên CPU.

Vì vậy, một function chỉ dùng một phần nhỏ RAM vẫn có thể chạy nhanh hơn ở mức memory cao hơn do nhận thêm CPU.

## 2. AWS Lambda tính chi phí như thế nào?

Chi phí Lambda thông thường gồm:

* Số lượng request.
* Thời gian thực thi dựa trên memory đã cấu hình.

Phần compute có thể được hiểu đơn giản qua công thức:

```text
Compute usage ∝ Memory được cấp × Thời gian chạy
```

Đơn vị thường dùng là GB-second.

Do đó, không thể kết luận một cấu hình rẻ hơn nếu chỉ nhìn vào lượng memory. Cần xem cả thời gian thực thi.

## 3. Ví dụ memory cao hơn nhưng compute thấp hơn

Giả sử một Lambda function xử lý file CSV.

### Cấu hình thứ nhất

```text
Memory: 128 MB = 0,125 GB
Thời gian: 4 giây
Compute: 0,125 × 4 = 0,5 GB-second
```

### Cấu hình thứ hai

```text
Memory: 512 MB = 0,5 GB
Thời gian: 0,8 giây
Compute: 0,5 × 0,8 = 0,4 GB-second
```

Trong ví dụ giả định này, cấu hình 512 MB có memory cao gấp bốn lần nhưng thời gian chạy giảm năm lần.

Kết quả:

* Function phản hồi nhanh hơn.
* Tổng GB-second thấp hơn.
* Chi phí compute có thể thấp hơn.

Điều này không xảy ra với mọi workload, nhưng cho thấy mức memory thấp nhất chưa chắc là lựa chọn tiết kiệm nhất.

## 4. Vì sao tăng memory có thể làm function nhanh hơn?

Nhiều workload được hưởng lợi trực tiếp từ CPU bổ sung:

* Parse JSON hoặc CSV lớn.
* Nén và giải nén dữ liệu.
* Resize ảnh.
* Mã hóa dữ liệu.
* Xử lý nhiều record.
* Import thư viện lớn.
* Tính toán số liệu.
* Machine learning inference nhỏ.

Một function có thể không dùng hết RAM nhưng vẫn bị giới hạn bởi CPU.

Ví dụ CloudWatch log hiển thị:

```text
Memory Size: 512 MB
Max Memory Used: 150 MB
```

Thông tin này không đủ để kết luận nên giảm xuống 256 MB. Function có thể đang cần lượng CPU được cấp kèm với cấu hình 512 MB.

## 5. Khi nào tăng memory mang lại hiệu quả rõ?

### Function CPU-bound

Các tác vụ dành phần lớn thời gian cho tính toán thường có khả năng giảm duration khi tăng memory:

* Resize ảnh.
* Nén file.
* Xử lý âm thanh.
* Mã hóa.
* Parse dữ liệu lớn.
* Tính toán phức tạp.

### Function memory-bound

Function sử dụng gần hết memory có thể chạy không ổn định hoặc gặp lỗi. Tăng memory giúp có thêm không gian xử lý dữ liệu và thư viện.

### Function dùng thư viện lớn

Các thư viện như pandas, NumPy hoặc thư viện xử lý ảnh có thể cần nhiều tài nguyên trong quá trình import và xử lý.

### Function thực hiện nhiều I/O

Một số workload truy cập S3, EFS hoặc mạng cũng có thể được cải thiện khi tăng memory. Tuy nhiên, mức cải thiện phụ thuộc vào điểm nghẽn thực tế.

## 6. Khi nào tăng memory làm chi phí cao hơn?

Nếu function chủ yếu chờ một dịch vụ bên ngoài, thêm CPU có thể không làm giảm duration đáng kể.

Ví dụ:

```text
128 MB chạy khoảng 2 giây
1.024 MB vẫn chạy khoảng 2 giây
```

Nếu nguyên nhân chính là chờ API hoặc database, memory tăng nhiều lần nhưng thời gian gần như không đổi. Khi đó, chi phí compute sẽ tăng.

Một số workload có thể ít hưởng lợi:

* Chờ API bên ngoài.
* Chờ database có độ trễ cố định.
* Chuyển tiếp một message nhỏ.
* Logic rất đơn giản.
* Tác vụ bị giới hạn bởi hệ thống phía sau.

## 7. Cách tìm mức memory phù hợp

Không có một mức memory tối ưu cho mọi Lambda function.

Có thể thực hiện theo các bước:

1. Chuẩn bị request đại diện cho workload thực tế.
2. Chạy function ở nhiều mức memory.
3. Ghi lại `Duration`, `Billed Duration` và `Max Memory Used`.
4. Tính GB-second cho từng cấu hình.
5. So sánh cả độ trễ và chi phí.
6. Chọn mức phù hợp với mục tiêu của hệ thống.

Không nên chỉ chạy một lần vì kết quả có thể bị ảnh hưởng bởi cold start hoặc dữ liệu đầu vào.

Nên kiểm thử nhiều lần với:

* Dữ liệu nhỏ.
* Dữ liệu trung bình.
* Dữ liệu lớn.
* Trường hợp cold start và warm start.

## 8. AWS Lambda Power Tuning

AWS Lambda Power Tuning là công cụ mã nguồn mở giúp chạy function ở nhiều mức memory và so sánh:

* Memory.
* Thời gian thực thi.
* Chi phí.
* Hiệu suất.

Công cụ sử dụng AWS Step Functions để tự động hóa quá trình kiểm thử và có thể trực quan hóa kết quả.

Người dùng có thể lựa chọn theo mục tiêu:

```text
Chi phí thấp nhất
Thời gian nhanh nhất
Cân bằng chi phí và hiệu năng
```

Quá trình tuning gọi function thật trong tài khoản AWS, vì vậy vẫn có thể phát sinh chi phí kiểm thử.

## 9. AWS Compute Optimizer

AWS Compute Optimizer có thể phân tích lịch sử hoạt động và đưa ra đề xuất memory cho những Lambda function đủ điều kiện.

Đề xuất có thể cho biết function:

* Được cấp quá nhiều memory.
* Được cấp quá ít memory.
* Chưa có đủ dữ liệu để phân tích.

Theo tài liệu AWS, Lambda function cần đáp ứng các điều kiện nhất định về số lần gọi, lịch sử hoạt động, kiến trúc và cấu hình memory để nhận đề xuất.

Có thể phân biệt:

```text
Lambda Power Tuning
→ Chủ động benchmark function mới

AWS Compute Optimizer
→ Phân tích function đã có dữ liệu vận hành
```

Đề xuất từ công cụ vẫn nên được kiểm thử lại bằng workload đại diện trước khi áp dụng.

## 10. Ví dụ thực tế

Giả sử một nhóm có Lambda function đọc file CSV, làm sạch dữ liệu rồi tạo file kết quả.

Ban đầu function được đặt ở 128 MB để tiết kiệm. Khi file tăng kích thước, duration tăng và đôi lúc gần chạm timeout.

Nhóm thử:

```text
128 MB
256 MB
512 MB
1.024 MB
```

Kết quả giả định:

* 128 MB: chạy lâu vì thiếu CPU.
* 256 MB: nhanh hơn nhưng chưa ổn định.
* 512 MB: duration giảm mạnh và tổng GB-second thấp nhất.
* 1.024 MB: nhanh hơn một chút nhưng chi phí bắt đầu tăng.

Trong trường hợp này, 512 MB là điểm cân bằng tốt hơn giữa thời gian chạy và chi phí.

## 11. Các lỗi dễ gặp

* Luôn giữ mặc định 128 MB.
* Chỉ nhìn vào `Max Memory Used`.
* Tăng memory nhưng không đo lại duration.
* Chỉ thử với một loại dữ liệu.
* Không phân biệt cold start và thời gian xử lý.
* Chỉ quan tâm chi phí mà bỏ qua độ trễ.
* Áp dụng đề xuất trực tiếp vào môi trường chính mà chưa kiểm thử.

## Kết luận

Memory trong AWS Lambda không chỉ là dung lượng RAM. Tăng memory cũng có thể cung cấp thêm CPU và làm giảm thời gian thực thi.

Vì chi phí compute phụ thuộc vào cả memory và duration, một cấu hình memory cao hơn vẫn có thể rẻ hơn nếu function hoàn thành nhanh hơn đủ nhiều.

Tuy nhiên, tăng memory không phải giải pháp cho mọi workload. Nếu function chủ yếu chờ API hoặc database bên ngoài, thời gian chạy có thể không giảm đủ để bù lại memory tăng thêm.

Thay vì hỏi:

> Mức memory thấp nhất là bao nhiêu?

Câu hỏi phù hợp hơn là:

> Mức memory nào tạo ra sự cân bằng tốt nhất giữa thời gian chạy, độ ổn định và chi phí?

## Tài liệu tham khảo

* [Configuring Lambda function memory](https://docs.aws.amazon.com/lambda/latest/dg/configuration-memory.html)
* [Best practices for working with AWS Lambda functions](https://docs.aws.amazon.com/lambda/latest/dg/best-practices.html)
* [AWS Lambda Power Tuning](https://github.com/alexcasalboni/aws-lambda-power-tuning)
* [AWS Lambda Pricing](https://aws.amazon.com/lambda/pricing/)
* [Viewing recommendations for Lambda functions in AWS Compute Optimizer](https://docs.aws.amazon.com/compute-optimizer/latest/ug/view-lambda-recommendations.html)
