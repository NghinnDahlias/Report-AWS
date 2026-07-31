---
title: "Blog 1"
date: 2026-07-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}

# IAM ROLE CÓ QUYỀN NHƯNG AWS SERVICE VẪN KHÔNG DÙNG ĐƯỢC?

Trong quá trình thực tập và làm việc với AWS dưới góc nhìn DevOps, một trong những vấn đề khiến mình mất nhiều thời gian nhất là cấu hình quyền truy cập giữa các AWS services.

Ban đầu, mình cho rằng chỉ cần tạo một IAM Role, gắn permission cần thiết rồi chọn role đó cho service là hệ thống có thể hoạt động. Tuy nhiên, trên thực tế, một role có đầy đủ permission vẫn có thể không được AWS service sử dụng.

Nguyên nhân thường nằm ở ba thành phần:

* Trust Policy.
* Permission Policy.
* Quyền `iam:PassRole` của người cấu hình tài nguyên.

## Các khái niệm chính cần nắm

### Trust Policy

Trust Policy xác định principal nào được phép sử dụng hoặc assume IAM Role.

Có thể hiểu đơn giản:

> Trust Policy trả lời câu hỏi: “Ai được phép sử dụng role này?”

Ví dụ, một AWS service giả định cần sử dụng role:

```json
{
  "Version": "2026-07-01",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "service-a.amazonaws.com"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
```

Nếu service principal được khai báo không đúng, service sẽ không thể sử dụng role, kể cả khi role đã có đầy đủ permission.

### Permission Policy

Permission Policy xác định role được phép thực hiện hành động nào trên tài nguyên nào sau khi được assume.

Có thể hiểu:

> Permission Policy trả lời câu hỏi: “Sau khi sử dụng role, principal được phép làm gì?”

Ví dụ:

```json
{
  "Version": "2026-07-01",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "service-b:WriteData",
      "Resource": "arn:aws:service-b:region:123456789012:resource/example"
    }
  ]
}
```

Một service role chỉ hoạt động đúng khi cả Trust Policy và Permission Policy đều được cấu hình chính xác.

```text
Trust Policy đúng
        +
Permission Policy đúng
        =
AWS service sử dụng được role
```

## `iam:PassRole` là gì?

Một vấn đề khác thường gặp là người dùng có quyền tạo hoặc cấu hình AWS resource nhưng không thể chọn IAM Role cho resource đó.

Khi một người chỉ định role để AWS service sử dụng, người đó không trực tiếp assume role. Thay vào đó, họ đang chuyển role cho service thông qua hành động:

```text
iam:PassRole
```

Ví dụ policy giới hạn quyền pass một role cụ thể:

```json
{
  "Version": "2026-07-01",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "iam:PassRole",
      "Resource": "arn:aws:iam::123456789012:role/example-service-role",
      "Condition": {
        "StringEquals": {
          "iam:PassedToService": "service-a.amazonaws.com"
        }
      }
    }
  ]
}
```

Không nên cấp quyền quá rộng như:

```json
{
  "Effect": "Allow",
  "Action": "iam:PassRole",
  "Resource": "*"
}
```

Quyền `iam:PassRole` quá rộng có thể cho phép người dùng gán một role mạnh hơn phạm vi công việc của họ cho AWS service.

## Phân biệt `iam:PassRole` và `sts:AssumeRole`

Hai hành động này thường bị nhầm lẫn nhưng có mục đích khác nhau.

### `sts:AssumeRole`

Được sử dụng khi một user, application hoặc AWS service trực tiếp nhận temporary credentials của role.

```text
Principal
→ AssumeRole
→ Nhận temporary credentials
→ Thực hiện hành động theo permission của role
```

### `iam:PassRole`

Được sử dụng khi một người cấu hình AWS resource và chỉ định role để AWS service sử dụng.

```text
Người cấu hình
→ PassRole
→ AWS service nhận role
→ AWS service assume role
```

Nói ngắn gọn:

```text
AssumeRole:
Principal trực tiếp sử dụng role.

PassRole:
Principal giao role cho AWS service sử dụng.
```

## Checklist khi AWS service không sử dụng được IAM Role

Khi gặp lỗi liên quan đến role, thay vì cấp thêm quyền quản trị, mình thường kiểm tra lần lượt:

* Trust Policy có đúng service principal hay không.
* Permission Policy có chứa đúng action cần thiết hay không.
* Resource ARN có đúng account, region và resource hay không.
* Người cấu hình có quyền `iam:PassRole` hay không.
* Quyền `iam:PassRole` có áp dụng cho đúng role hay không.
* Điều kiện `iam:PassedToService` có đúng service hay không.
* Role có bị giới hạn bởi Permissions Boundary hay không.
* Có Explicit Deny từ policy khác hay không.

Quy trình kiểm tra tổng quát:

```text
Người cấu hình
→ Có quyền PassRole
→ AWS service được Trust
→ Service assume role
→ Role có permission phù hợp
→ Resource đích cho phép hành động
```

## Bài học rút ra

Trước khi làm việc thực tế với AWS, mình thường hình dung IAM theo luồng đơn giản:

```text
User
→ Policy
→ Permission
```

Sau quá trình triển khai, mình nhận ra một luồng cấp quyền giữa các AWS services có thể gồm nhiều lớp hơn:

```text
Người cấu hình
→ Pass role cho AWS service
→ AWS service được phép assume role
→ Role thực hiện action được cấp
→ Tài nguyên đích tiếp nhận request
```

Vì vậy, khi một role không hoạt động, không nên chỉ kiểm tra Permission Policy.

Ba thành phần quan trọng cần kiểm tra đồng thời là:

* Trust Policy: Ai được phép sử dụng role?
* Permission Policy: Role được phép làm gì?
* `iam:PassRole`: Ai được phép giao role cho AWS service?

## Áp dụng nguyên tắc Least Privilege

Thay vì cấp các policy quá rộng như:

```text
AdministratorAccess
IAMFullAccess
AmazonS3FullAccess
```

DevOps nên giới hạn quyền theo:

* Đúng action.
* Đúng IAM Role.
* Đúng AWS service.
* Đúng resource ARN.
* Đúng môi trường triển khai.

Ví dụ:

```text
Không nên:
iam:PassRole trên tất cả role.

Nên:
iam:PassRole trên một role cụ thể,
đồng thời giới hạn service được nhận role.
```

Cách này vẫn đảm bảo thành viên có thể hoàn thành công việc nhưng giảm nguy cơ sử dụng nhầm hoặc lạm dụng quyền.

## Kết luận

Bài học quan trọng nhất mình rút ra là:

> Một IAM Role có permission chưa chắc đã sử dụng được. AWS service còn phải được Trust Policy cho phép assume role, và người cấu hình có thể cần quyền `iam:PassRole`.

IAM không đơn thuần là cấp quyền để hệ thống chạy được. Một thiết kế IAM tốt phải xác định rõ:

```text
Ai
→ được sử dụng role nào
→ để thực hiện hành động gì
→ trên tài nguyên nào
```

Việc hiểu đúng Trust Policy, Permission Policy và `iam:PassRole` giúp quá trình debug nhanh hơn, hạn chế cấp quyền quá rộng và hỗ trợ áp dụng nguyên tắc least privilege hiệu quả hơn.

## Đường dẫn dến bài viết gốc


## Tài liệu tham khảo

* [AWS IAM Roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html)
* [Grant a user permissions to pass a role to an AWS service](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_passrole.html)
* [IAM Policies and Permissions](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html)
* [IAM Security Best Practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)
* [Troubleshooting IAM Roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/troubleshoot_roles.html)
