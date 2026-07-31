---

title: "Tự đánh giá"
date: 2024-01-01
weight: 6
chapter: false
pre: " <b> 6. </b> "
--------------------

{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn, kể cả nội dung cảnh báo này.
{{% /notice %}}

Sau 8 tuần thực tập tại chương trình **AWS First Cloud AI Journey**, với vai trò **DevOps/QA & Documentation** trong nhóm thực hiện **Đề tài 5 – Machine Learning on AWS**, em đã có cơ hội vận dụng kiến thức đã học vào quá trình xây dựng và vận hành một hệ thống Machine Learning thực tế trên nền tảng AWS.

Trong quá trình thực tập, em tham gia quản lý môi trường AWS của nhóm, thiết lập quyền truy cập, theo dõi chi phí, hỗ trợ triển khai Backend, giám sát hệ thống, kiểm thử tích hợp, tổng hợp tài liệu và chuẩn bị nội dung demo. Qua đó, em hiểu rõ hơn mối liên hệ giữa hạ tầng cloud, dữ liệu, mô hình Machine Learning, Backend và hoạt động vận hành hệ thống.

## 1. Sản phẩm, kỹ năng và kiến thức thu nhận được

### Kiến thức chuyên môn

Qua quá trình thực hiện dự án, em đã tiếp thu và củng cố được các kiến thức sau:

* Hiểu kiến trúc end-to-end của một hệ thống Machine Learning trên AWS, bao gồm luồng dữ liệu từ **AWS IoT Core**, **Amazon Data Firehose**, **Amazon S3**, **Amazon SageMaker Processing**, **SageMaker Endpoint**, **FastAPI** đến **Amazon SNS**.
* Hiểu cách tổ chức và quản lý tài khoản AWS theo hướng an toàn, bao gồm **root account**, **MFA**, **IAM User**, **IAM Group**, **IAM Role** và nguyên tắc **least privilege**.
* Hiểu vai trò của IAM Service Role trong việc cho phép các dịch vụ AWS tương tác với nhau mà không cần lưu trực tiếp access key trong mã nguồn.
* Biết cách triển khai Backend trên Amazon EC2, cấu hình Security Group và sử dụng IAM Instance Role.
* Biết cách sử dụng Amazon CloudWatch để thu thập log, theo dõi metric, xây dựng dashboard và truy vấn lỗi bằng CloudWatch Logs Insights.
* Hiểu quy trình kiểm thử integration và end-to-end đối với một hệ thống gồm nhiều thành phần.
* Hiểu tầm quan trọng của Resource Inventory, naming convention, tagging, log retention, AWS Budgets và cleanup trong việc quản lý tài nguyên và chi phí cloud.
* Có thêm kinh nghiệm lựa chọn, cấu hình và vận hành tài nguyên AWS dựa trên yêu cầu kỹ thuật, bảo mật và ngân sách của dự án.

### Kỹ năng đạt được

Trong quá trình thực tập, em đã rèn luyện được các kỹ năng sau:

* Quản lý IAM User, IAM Group, IAM Role và policy trên AWS.
* Cấu hình Amazon EC2, Security Group và IAM Instance Profile.
* Thiết lập AWS Budgets và theo dõi chi phí phát sinh.
* Sử dụng CloudWatch Logs, CloudWatch Metrics, CloudWatch Dashboard và Logs Insights.
* Kiểm thử integration và end-to-end cho hệ thống gồm nhiều module.
* Phân tích log để xác định vị trí và nguyên nhân gây lỗi.
* Xây dựng test case cho dữ liệu hợp lệ, dữ liệu không hợp lệ, service failure và trường hợp vượt ngưỡng cảnh báo.
* Quản lý tài nguyên theo naming convention, tag convention và Resource Inventory.
* Viết tài liệu kỹ thuật như README, Runbook, Architecture Document, Test Report và Cost/Cleanup Document.
* Phối hợp với các thành viên phụ trách Ingestion, Data, Machine Learning và Backend.
* Điều phối tiến độ, tổng hợp tài liệu, chuẩn bị nội dung và kịch bản demo nhóm.
* Trình bày, báo cáo tiến độ và trao đổi vấn đề kỹ thuật với các thành viên trong nhóm.

### Sản phẩm đạt được

Các sản phẩm em đã tham gia xây dựng và hoàn thiện gồm:

* Hệ thống IAM và phân quyền cơ bản cho tài khoản AWS của nhóm.
* AWS Budget và cơ chế theo dõi chi phí của dự án.
* Bộ quy tắc naming convention và tag convention cho tài nguyên AWS.
* Resource Inventory dùng để theo dõi tài nguyên, chủ sở hữu, trạng thái và quy tắc cleanup.
* EC2 Instance và môi trường triển khai FastAPI phục vụ quá trình kiểm thử và demo.
* CloudWatch Log Groups, Logs Insights Query và Dashboard giám sát hệ thống.
* Bộ test case và báo cáo kiểm thử end-to-end.
* Bộ tài liệu dự án gồm tài liệu kiến trúc, contract, runbook, hướng dẫn triển khai và cleanup.
* Kịch bản demo, ảnh chụp và video dự phòng.
* Báo cáo kiểm tra chi phí và bằng chứng cleanup tài nguyên AWS sau khi hoàn thành demo.

## 2. Cảm nhận cá nhân

Chương trình **AWS First Cloud AI Journey** được tổ chức tương đối bài bản, cung cấp hệ thống tài liệu và bài lab giúp sinh viên có cơ hội tiếp cận các dịch vụ cloud thông qua quá trình thực hành trực tiếp. Khi gặp khó khăn về kỹ thuật hoặc chưa xác định được hướng triển khai phù hợp, em nhận được sự hỗ trợ từ mentor và các thành viên trong nhóm để từng bước hoàn thiện nhiệm vụ được giao.

Điểm khác biệt lớn nhất so với việc học lý thuyết tại trường là em phải trực tiếp quản lý và vận hành tài nguyên trên một tài khoản AWS thật. Mỗi cấu hình IAM, EC2, SageMaker Endpoint hoặc CloudWatch Log Group đều có thể ảnh hưởng đến bảo mật, khả năng hoạt động và chi phí của toàn bộ dự án. Vì vậy, em không chỉ tìm hiểu cách tạo tài nguyên mà còn phải quan tâm đến quyền truy cập, khả năng giám sát, cách xử lý lỗi và quy trình dừng hoặc xóa tài nguyên sau khi sử dụng.

Khó khăn lớn nhất em gặp phải là việc thiết kế quyền IAM phù hợp cho từng thành viên và từng dịch vụ. Nếu cấp quyền quá ít, các thành viên có thể không hoàn thành được nhiệm vụ. Ngược lại, nếu cấp quyền quá rộng, tài khoản có thể gặp rủi ro bảo mật hoặc phát sinh tài nguyên ngoài kiểm soát. Để khắc phục, em phân tích luồng tương tác giữa các dịch vụ, xác định quyền cần thiết cho từng tác vụ và tạo IAM Role theo từng mục đích cụ thể.

Một khó khăn khác là quá trình kiểm thử end-to-end liên quan đến nhiều thành phần do các thành viên khác nhau phụ trách. Một lỗi được phát hiện tại Backend chưa chắc bắt nguồn từ Backend mà có thể xuất phát từ dữ liệu đầu vào, Firehose, Processing Job, quyền truy cập S3 hoặc SageMaker Endpoint. Việc thiết lập CloudWatch Logs và thống nhất định dạng log giúp em xác định được lỗi nằm ở module nào thay vì phải kiểm tra thủ công toàn bộ hệ thống.

Điều em tâm đắc nhất sau kỳ thực tập là hiểu rằng DevOps không chỉ dừng lại ở việc triển khai một máy chủ hoặc cấu hình tài khoản AWS. DevOps còn bao gồm việc xây dựng môi trường để các thành viên có thể làm việc an toàn, theo dõi được trạng thái hệ thống, kiểm soát chi phí, xử lý sự cố, kiểm thử khả năng tích hợp và bảo đảm tài nguyên được cleanup sau khi dự án hoàn thành.

Thông qua vai trò **DevOps/QA & Documentation**, em có cơ hội quan sát toàn bộ hệ thống thay vì chỉ tập trung vào một module riêng lẻ. Điều này giúp em hình thành tư duy hệ thống và hiểu rõ hơn mối liên hệ giữa hạ tầng, dữ liệu, mô hình Machine Learning, Backend và hoạt động vận hành thực tế trên cloud.

## 3. Tự đánh giá

Để phản ánh khách quan quá trình thực tập, em xin tự đánh giá bản thân dựa trên các tiêu chí sau:

| STT | Tiêu chí                            | Mô tả                                                                                           | Tốt | Khá | Trung bình |
| --- | ----------------------------------- | ----------------------------------------------------------------------------------------------- | --- | --- | ---------- |
| 1   | **Kiến thức và kỹ năng chuyên môn** | Hiểu kiến trúc hệ thống, sử dụng công cụ AWS và áp dụng kiến thức vào công việc thực tế         | ✅   | ☐   | ☐          |
| 2   | **Khả năng học hỏi**                | Chủ động tiếp thu kiến thức mới và tìm hiểu các dịch vụ AWS chưa từng sử dụng                   | ✅   | ☐   | ☐          |
| 3   | **Tính chủ động**                   | Tự tìm hiểu tài liệu, đề xuất hướng triển khai và thực hiện nhiệm vụ mà không phụ thuộc chỉ dẫn | ✅   | ☐   | ☐          |
| 4   | **Tinh thần trách nhiệm**           | Theo dõi nhiệm vụ, hỗ trợ nhóm và cố gắng hoàn thành công việc theo đúng tiến độ                | ✅   | ☐   | ☐          |
| 5   | **Kỷ luật**                         | Tuân thủ giờ giấc, nội quy và kế hoạch làm việc của chương trình                                | ☐   | ✅   | ☐          |
| 6   | **Tính cầu tiến**                   | Sẵn sàng tiếp nhận góp ý, sửa lỗi và cải thiện chất lượng công việc                             | ✅   | ☐   | ☐          |
| 7   | **Giao tiếp**                       | Trình bày ý tưởng, báo cáo tiến độ và trao đổi vấn đề với các thành viên                        | ☐   | ✅   | ☐          |
| 8   | **Hợp tác nhóm**                    | Phối hợp với các thành viên phụ trách Ingestion, Data, Machine Learning và Backend              | ✅   | ☐   | ☐          |
| 9   | **Ứng xử chuyên nghiệp**            | Tôn trọng mentor, thành viên nhóm và có thái độ nghiêm túc trong quá trình làm việc             | ✅   | ☐   | ☐          |
| 10  | **Tư duy giải quyết vấn đề**        | Phân tích lỗi, tìm nguyên nhân và đề xuất phương án khắc phục phù hợp                           | ☐   | ✅   | ☐          |
| 11  | **Đóng góp vào dự án**              | Tham gia quản lý hạ tầng, kiểm thử, giám sát, tài liệu và chuẩn bị demo                         | ✅   | ☐   | ☐          |
| 12  | **Đánh giá tổng thể**               | Hoàn thành tương đối tốt vai trò DevOps/QA & Documentation trong phạm vi dự án                  | ✅   | ☐   | ☐          |

## 4. Nội dung cần cải thiện

Bên cạnh những kiến thức và kỹ năng đã đạt được, em nhận thấy bản thân vẫn cần tiếp tục cải thiện ở một số mặt sau:

* Nâng cao tính kỷ luật, quản lý thời gian tốt hơn và chấp hành nghiêm túc nội quy của công ty hoặc tổ chức.
* Cải thiện khả năng lập kế hoạch và phân chia mức độ ưu tiên cho từng nhiệm vụ.
* Rèn luyện tư duy giải quyết vấn đề theo hướng có hệ thống, xác định nguyên nhân gốc thay vì chỉ xử lý biểu hiện của lỗi.
* Cải thiện khả năng giao tiếp trong công việc, đặc biệt là cách trình bày vấn đề ngắn gọn, rõ ràng và đúng trọng tâm.
* Chủ động báo cáo sớm khi gặp trở ngại để tránh ảnh hưởng đến tiến độ chung của nhóm.
* Tiếp tục nâng cao kiến thức về AWS, DevOps, bảo mật cloud, monitoring và tự động hóa triển khai.
* Rèn luyện thêm khả năng xử lý tình huống và phối hợp khi có sự khác biệt về quan điểm giữa các thành viên.

## 5. Kết luận

Kỳ thực tập tại chương trình **AWS First Cloud AI Journey** đã giúp em có thêm trải nghiệm thực tế trong việc triển khai và vận hành một hệ thống Machine Learning trên AWS. Bên cạnh kiến thức chuyên môn, em còn rèn luyện được kỹ năng phối hợp nhóm, kiểm thử hệ thống, quản lý tài nguyên, viết tài liệu và xử lý các vấn đề phát sinh trong quá trình thực hiện dự án.

Những kiến thức, kỹ năng và kinh nghiệm thu nhận được trong kỳ thực tập là nền tảng quan trọng để em tiếp tục học tập, cải thiện bản thân và định hướng phát triển trong lĩnh vực Cloud Computing, DevOps và Machine Learning trong tương lai.
