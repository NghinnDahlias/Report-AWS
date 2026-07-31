---
title: "Blog 1"
date: 2026-07-30
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}


# TẠI SAO REST API KHÔNG PHẢI LÚC NÀO CŨNG TỐT? SỨC MẠNH CỦA PUB/SUB VÀ MQTT TRONG HỆ THỐNG PHÂN TÁN

Khi thiết kế hệ thống giao tiếp giữa các service, client hoặc thiết bị, REST API qua HTTP thường là lựa chọn đầu tiên. Client gửi request, server xử lý rồi trả về response. Mô hình này quen thuộc, dễ triển khai và phù hợp với nhiều ứng dụng truyền thống.

Tuy nhiên, khi hệ thống mở rộng, đặc biệt là khi cần xử lý dữ liệu thời gian thực từ nhiều thiết bị hoặc tích hợp nhiều dịch vụ độc lập, mô hình request/response đồng bộ bắt đầu bộc lộ một số hạn chế.

Pub/Sub và MQTT là những hướng tiếp cận phù hợp hơn cho các bài toán cần giao tiếp bất đồng bộ, giảm phụ thuộc giữa các thành phần và mở rộng theo kiến trúc event-driven.

## 1. Hạn chế của mô hình đồng bộ HTTP/REST

Trong mô hình REST, client thường phải chủ động gửi request đến server. Nếu muốn kiểm tra xem có dữ liệu hoặc lệnh mới hay không, client có thể phải thực hiện polling liên tục.

Một số vấn đề dễ gặp:

* Request có thể bị timeout khi mạng không ổn định.
* Polling liên tục làm tăng số lượng request và băng thông sử dụng.
* Client và server phụ thuộc trực tiếp vào trạng thái hoạt động của nhau.
* Khi một service gặp sự cố, service gọi trực tiếp đến nó có thể bị lỗi theo.
* Việc mở rộng thêm nhiều consumer thường đòi hỏi sửa đổi logic hiện có.

Mô hình này vẫn hiệu quả với các tác vụ như truy vấn dữ liệu, đăng nhập, gửi biểu mẫu hoặc các thao tác cần phản hồi ngay. Tuy nhiên, nó không phải lúc nào cũng phù hợp với dữ liệu telemetry hoặc luồng sự kiện liên tục.

## 2. Pub/Sub và MQTT giải quyết vấn đề như thế nào?

Trong mô hình Publish/Subscribe, một broker đứng giữa publisher và subscriber.

### Publisher

Publisher chỉ cần gửi message vào một topic cụ thể. Publisher không cần biết:

* Có bao nhiêu subscriber.
* Subscriber đang chạy ở đâu.
* Subscriber xử lý dữ liệu như thế nào.

### Subscriber

Subscriber đăng ký theo dõi topic. Khi broker nhận message mới, message sẽ được phân phối đến subscriber phù hợp.

```text
Publisher
→ Topic
→ Message Broker
→ Subscriber
```

Cách tổ chức này tạo ra sự tách biệt giữa các thành phần:

```text
Publisher không cần gọi trực tiếp Subscriber
Subscriber không cần biết Publisher cụ thể
Broker chịu trách nhiệm phân phối message
```

MQTT được thiết kế theo hướng nhẹ, phù hợp với thiết bị hạn chế tài nguyên hoặc kết nối mạng không ổn định. Payload và phần header của MQTT thường nhỏ hơn nhiều giao thức ứng dụng truyền thống, giúp giảm chi phí truyền dữ liệu.

## 3. Event-Driven Architecture trên AWS

Tư duy Pub/Sub không chỉ áp dụng cho thiết bị IoT mà còn có thể được sử dụng trong backend và hệ thống phân tán.

Một số dịch vụ AWS thường gặp:

### AWS IoT Core

AWS IoT Core cung cấp MQTT broker được quản lý, hỗ trợ thiết bị kết nối an toàn bằng certificate và định tuyến message bằng AWS IoT Rules Engine.

### Amazon SNS

Amazon Simple Notification Service hỗ trợ mô hình Pub/Sub và fan-out. Một message có thể được gửi đến nhiều subscriber như SQS, Lambda, HTTP endpoint hoặc email.

### Amazon EventBridge

Amazon EventBridge cung cấp event bus để kết nối AWS services, ứng dụng riêng và một số nền tảng SaaS thông qua event.

Ba dịch vụ này đều liên quan đến event-driven nhưng phục vụ các phạm vi khác nhau:

```text
AWS IoT Core
→ Kết nối và định tuyến message từ thiết bị

Amazon SNS
→ Pub/Sub và fan-out thông báo

Amazon EventBridge
→ Định tuyến sự kiện giữa ứng dụng và dịch vụ
```

## 4. Ví dụ luồng dữ liệu IoT

Một luồng dữ liệu tổng quát có thể được thiết kế như sau:

```text
MQTT Gateway
→ AWS IoT Core
→ AWS IoT Rules Engine
→ Amazon Data Firehose
→ Amazon S3
```

Các bước xử lý:

1. Gateway gửi telemetry đến AWS IoT Core qua MQTT.
2. AWS IoT Rules Engine nhận message theo topic đã cấu hình.
3. Rule chuyển dữ liệu đến Amazon Data Firehose.
4. Firehose gom nhiều record và lưu dữ liệu vào Amazon S3.
5. Một rule hoặc nhánh xử lý khác có thể gọi Lambda khi dữ liệu vượt ngưỡng.

Ví dụ cảnh báo:

```text
Telemetry Event
→ Rule kiểm tra điều kiện
→ AWS Lambda
→ Dịch vụ gửi thông báo
```

Trong kiến trúc này, gateway không cần gọi trực tiếp database hoặc hệ thống cảnh báo. Các thành phần được kích hoạt thông qua event và có thể được mở rộng độc lập.

## 5. Khi nào nên dùng REST và khi nào nên dùng Pub/Sub?

### REST phù hợp khi

* Client cần phản hồi ngay.
* Thao tác mang tính truy vấn hoặc command rõ ràng.
* Cần giao tiếp request/response đơn giản.
* Số lượng thành phần tham gia chưa quá lớn.
* Người gọi cần biết kết quả thành công hoặc thất bại ngay lập tức.

### Pub/Sub phù hợp khi

* Dữ liệu được phát sinh liên tục.
* Nhiều consumer cần nhận cùng một event.
* Các thành phần cần hoạt động độc lập.
* Hệ thống cần xử lý bất đồng bộ.
* Muốn bổ sung consumer mới mà không sửa publisher.
* Cần xây dựng kiến trúc event-driven.

REST và Pub/Sub không loại trừ nhau. Một hệ thống thực tế có thể sử dụng REST cho API người dùng và Pub/Sub cho giao tiếp nội bộ hoặc xử lý sự kiện.

## Kết luận

REST API vẫn là lựa chọn phù hợp cho nhiều mô hình client-server truyền thống. Tuy nhiên, với IoT, gateway phân tán, telemetry và microservices, giao tiếp đồng bộ có thể làm tăng sự phụ thuộc giữa các thành phần.

Pub/Sub và MQTT giúp hệ thống:

* Giảm tight coupling.
* Xử lý dữ liệu bất đồng bộ.
* Dễ mở rộng thêm subscriber.
* Phù hợp với thiết bị và mạng hạn chế.
* Hỗ trợ kiến trúc event-driven.

Điểm quan trọng không phải là thay thế REST hoàn toàn, mà là lựa chọn đúng mô hình giao tiếp cho từng loại workload.

## Tài liệu tham khảo

* [What is AWS IoT Core?](https://docs.aws.amazon.com/iot/latest/developerguide/what-is-aws-iot.html)
* [MQTT topics](https://docs.aws.amazon.com/iot/latest/developerguide/topics.html)
* [AWS IoT Rules](https://docs.aws.amazon.com/iot/latest/developerguide/iot-rules.html)
* [What is Amazon SNS?](https://docs.aws.amazon.com/sns/latest/dg/welcome.html)
* [What is Amazon EventBridge?](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-what-is.html)
* [Amazon Data Firehose](https://docs.aws.amazon.com/firehose/latest/dev/what-is-this-service.html)
