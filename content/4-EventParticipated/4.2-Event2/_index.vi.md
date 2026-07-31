---
title: "Event 2: Capstone Solution Presentation"
date: 2026-07-25
weight: 1
chapter: false
pre: " <b> 4.2. </b> "
---

{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}

# Bài thu hoạch sự kiện chia sẻ Agentic AI Build Week và AWS Community Day

### Mục Đích Của Sự Kiện

- Chia sẻ hành trình xây dựng sản phẩm AI trên AWS từ ý tưởng đến bản demo.
- Giới thiệu các bài toán thực tế có thể giải quyết bằng Agentic AI, Computer Vision và kiến trúc cloud-native.
- Trình bày cách các nhóm thiết kế workflow, kiến trúc, chi phí và trải nghiệm người dùng.
- Chia sẻ những khó khăn khi làm việc nhóm, phát triển MVP trong thời gian ngắn và trình bày sản phẩm trước hội đồng.
- Truyền cảm hứng cho người mới bắt đầu tham gia hackathon, thử nghiệm AWS và phát triển sản phẩm AI có khả năng ứng dụng thực tế.

### Danh Sách Nhóm Và Nội Dung Trình Bày

- **One Team**: Xây dựng trợ lý đặt món hội thoại đa kênh KFC Bot Agent.
- **Plan V**: Xây dựng Solution Architect Professional AI Native App hỗ trợ phân tích yêu cầu, đề xuất kiến trúc, sinh sơ đồ và ước tính chi phí AWS.
- **SignalScout**: Xây dựng nền tảng phát hiện sớm thay đổi chiến lược doanh nghiệp dựa trên dữ liệu và bằng chứng.
- **3KA**: Chia sẻ hành trình hackathon và dự án S.H.E.P.H.E.R.D. hỗ trợ giám sát đám đông, dự báo tắc nghẽn và đề xuất hành động vận hành.

---

## Nội Dung Nổi Bật

### 1. Từ chatbot trả lời sang AI agent có khả năng hành động

Nhóm One Team trình bày bài toán đặt món qua hội thoại. Vấn đề không chỉ nằm ở khả năng hiểu ngôn ngữ tự nhiên mà còn ở việc xử lý:

- Món ăn, số lượng và biến thể.
- Trạng thái giỏ hàng.
- Quy tắc voucher và khuyến mãi.
- Xác nhận đơn hàng.
- Sai sót có thể dẫn đến ảnh hưởng tài chính thực tế.

Điểm nổi bật của giải pháp là phân biệt giữa chatbot và agent:

```text
Chatbot
→ Chủ yếu trả lời thông tin

AI Agent
→ Hiểu mục tiêu
→ Lập kế hoạch
→ Gọi công cụ
→ Cập nhật trạng thái thật
→ Kiểm tra kết quả
```

KFC Bot Agent được định hướng trở thành trợ lý đặt món đa kênh, cho phép khách hàng đặt món ngay trong nền tảng trò chuyện mà không cần chuyển ứng dụng hoặc tạo thêm tài khoản.

Nhóm cũng nhấn mạnh tư duy:

> Thiết kế một lần nhưng có thể mở rộng sang nhiều kênh, nhiều doanh nghiệp và nhiều capability khác nhau.

Kiến trúc tốt không chỉ giúp sản phẩm chạy được ở hiện tại mà còn cho phép thay đổi mà không phải xây lại toàn bộ hệ thống.

---

### 2. AI hỗ trợ công việc của Solution Architect

Nhóm Plan V tập trung vào một bài toán quen thuộc của Solution Architect: khách hàng đưa ra yêu cầu bằng ngôn ngữ tự nhiên và mong muốn nhanh chóng có kiến trúc, sơ đồ, chi phí cùng các khuyến nghị kỹ thuật.

Quy trình thủ công thường gồm:

- Đọc BRD hoặc PRD.
- Trích xuất yêu cầu.
- Xác định các khoảng trống thông tin.
- Phác thảo kiến trúc ban đầu.
- Vẽ sơ đồ.
- Ước tính chi phí.
- Điều chỉnh dựa trên phản hồi.

Giải pháp của nhóm hướng tới một AI Native App có khả năng:

- Phân tích yêu cầu tự nhiên và dữ liệu có cấu trúc.
- Tạo requirements catalogue.
- Đề xuất nhiều phương án kiến trúc cấp cao.
- Hỗ trợ kiến trúc hybrid cloud.
- Sinh sơ đồ Draw.io có thể chỉnh sửa.
- Sử dụng AWS Architecture Icons chính thức.
- Đưa ra ước tính chi phí định hướng theo region.
- Nêu rõ assumptions, recommendations và requirement gaps.
- Cho phép người dùng tiếp tục tinh chỉnh qua giao diện chat.

Giá trị lớn nhất của giải pháp không phải thay thế Solution Architect, mà là giúp tạo ra một bản nháp có căn cứ để review thay vì luôn bắt đầu từ trang trắng.

---

### 3. AI hỗ trợ phát hiện sớm thay đổi chiến lược doanh nghiệp

SignalScout giải quyết bài toán phân tích những tín hiệu phân tán liên quan đến hoạt động và chiến lược của doanh nghiệp.

Những nhóm người dùng mục tiêu gồm:

- Corporate strategy teams.
- Enterprise risk management teams.
- Competitive intelligence teams.
- B2B enterprise account management teams.

Giải pháp tập trung vào các giá trị:

- Phát hiện sớm thay đổi chiến lược.
- Nhận diện tín hiệu tái cấu trúc.
- Kết nối nhiều tín hiệu rời rạc thành một câu chuyện rõ ràng.
- Phân tích chỉ số tài chính và vận hành.
- Xây dựng timeline, cảnh báo rủi ro và scenario.
- Đưa ra khuyến nghị Maintain, Adapt hoặc Accelerate.
- Hỗ trợ mỗi kết luận bằng bằng chứng có thể kiểm tra.

Điểm đáng chú ý là nhóm đặt yếu tố **transparent and verifiable analysis** làm trọng tâm. AI không chỉ đưa ra kết luận mà phải liên kết kết luận với evidence để người dùng có thể kiểm chứng.

Nhóm cũng trình bày nhiều phương án chi phí và kiến trúc, qua đó cho thấy thiết kế hệ thống AI không chỉ là lựa chọn model mà còn phải cân bằng:

- Chi phí Bedrock và AgentCore.
- Chi phí hosting.
- Observability.
- Security.
- Data storage.
- Các dịch vụ bên thứ ba.
- Khả năng tối ưu kiến trúc theo nhiều mức tải.

---

### 4. Hành trình hackathon và bài toán giám sát đám đông

Nhóm 3KA chia sẻ dự án S.H.E.P.H.E.R.D.:

> Smart Human-flow Evaluation, Prediction, Hazard Detection, Response, and Dispatch.

Mục tiêu của hệ thống là biến camera giám sát thông thường thành nguồn thông tin vận hành có thể hành động được.

Các capability chính:

- Phát hiện và theo dõi người.
- Đo mật độ đám đông.
- Ước tính tình trạng hàng chờ.
- Nhận diện dấu hiệu tắc nghẽn.
- Dự báo nguy cơ quá tải.
- Tạo cảnh báo chủ động.
- Đề xuất điều phối nhân sự.

Giải pháp kết hợp:

- YOLO và ByteTrack.
- Amazon SageMaker.
- Amazon Bedrock AgentCore.
- Strands Agent.
- React Monitoring Dashboard.

Agentic AI layer được chia thành hai vai trò:

#### Autonomous Monitor

- Theo dõi liên tục các chỉ số đám đông.
- Nhận diện nguy cơ tắc nghẽn.
- Dự báo áp lực quá tải.
- Tạo cảnh báo chủ động.

#### Operator Copilot

- Cho phép nhân viên hỏi bằng ngôn ngữ tự nhiên.
- Trả lời dựa trên live metrics.
- Kết hợp công cụ dự báo và hành động vận hành.

---

## Những Gì Học Được

### Tư Duy Xây Dựng Sản Phẩm AI

- Bắt đầu từ vấn đề thực tế thay vì bắt đầu từ model hoặc dịch vụ AWS.
- AI chỉ thực sự có giá trị khi kết nối được với dữ liệu, business rules và hành động thật.
- Một bản demo tốt cần làm rõ luồng từ input đến output và giá trị người dùng nhận được.
- Agentic AI không đồng nghĩa với việc để model tự quyết định mọi thứ; cần có tools, guardrails và bước verification.
- Mỗi kết luận của AI trong các bài toán doanh nghiệp nên được hỗ trợ bằng dữ liệu hoặc evidence.

### Kiến Trúc Kỹ Thuật

- Tách hệ thống thành các thành phần độc lập giúp dễ mở rộng, thay thế và tái sử dụng.
- Multi-channel architecture nên sử dụng adapter thay vì viết lại toàn bộ business logic cho từng kênh.
- AI workflow nên tách rõ các bước hiểu yêu cầu, lập kế hoạch, gọi công cụ, hành động và xác minh.
- Observability là thành phần bắt buộc trong hệ thống phân tán và AI application.
- Việc lựa chọn dịch vụ phải xem xét đồng thời performance, scalability, security và cost.
- Kiến trúc tốt phải cho phép thay đổi sản phẩm mà không phải xây lại toàn bộ hệ thống.

### Quản Lý Phạm Vi MVP

Một bài học xuất hiện rõ trong các phần chia sẻ hackathon là:

> Sản phẩm nhỏ nhưng chạy hoàn chỉnh có giá trị hơn một ý tưởng lớn nhưng chưa hoạt động.

Để hoàn thành MVP trong thời gian ngắn cần:

- Xác định rõ mục tiêu.
- Chốt definition of done.
- Giảm số lượng tính năng.
- Ưu tiên luồng end-to-end.
- Chuẩn bị sẵn tài khoản, starter template và công cụ.
- Phân chia rõ người code, thiết kế, kiểm thử và thuyết trình.
- Chuẩn bị demo sớm thay vì chờ đến cuối.

### Làm Việc Nhóm

Những khó khăn được chia sẻ gồm:

- Thành viên chưa quen nhau.
- Không rõ ai phụ trách phần nào.
- Quên commit code.
- Code không hoạt động trong thời gian giới hạn.
- Thiếu kinh nghiệm AWS hoặc AI.
- Debug đến khuya và thiếu ngủ.
- Vô tình đẩy file môi trường lên GitHub.

Các tình huống này cho thấy DevOps và teamwork không chỉ là công cụ. Một nhóm cần:

- Naming và branching convention.
- Quy trình commit và review.
- Phân công owner.
- Quản lý secrets.
- Checklist triển khai.
- Kế hoạch demo và rollback.
- Giao tiếp thường xuyên giữa các thành viên.

---

## Ứng Dụng Vào Công Việc

### Áp dụng cho vai trò DevOps

- Chuẩn hóa repository, branch và commit workflow.
- Tách cấu hình môi trường khỏi source code.
- Không commit `.env`, credentials hoặc private key.
- Thiết lập CI để kiểm tra code trước khi merge.
- Chuẩn bị hạ tầng, tài khoản và quyền truy cập trước khi bắt đầu phát triển.
- Thiết lập CloudWatch Logs, metrics và cảnh báo từ đầu.
- Theo dõi chi phí của model, runtime và hạ tầng.
- Thiết kế kiến trúc theo module để mỗi thành viên có thể triển khai độc lập.
- Xây dựng checklist demo và cleanup tài nguyên sau sự kiện.

### Áp dụng cho dự án hiện tại

- Bắt đầu từ một luồng end-to-end nhỏ nhưng hoàn chỉnh.
- Tách phần thu thập dữ liệu, xử lý, AI và backend thành các module rõ ràng.
- Định nghĩa input, output và contract giữa các nhóm.
- Luôn có bước kiểm tra kết quả thật thay vì chỉ tin vào output của AI.
- Thiết kế hệ thống để có thể thay đổi nguồn dữ liệu, model hoặc kênh đầu ra mà không phải viết lại toàn bộ.
- Xây dựng dashboard hoặc evidence để chứng minh hệ thống đã hoạt động.
- Đánh giá chi phí từ sớm thay vì chỉ tính sau khi hoàn thành.

---

## Trải Nghiệm Trong Sự Kiện

Tham gia sự kiện giúp tôi hiểu rõ hơn cách một ý tưởng được chuyển thành sản phẩm AI có thể demo trong thực tế.

### Học từ các sản phẩm khác nhau

Bốn nhóm trình bày bốn bài toán rất khác nhau:

- Conversational commerce.
- Solution architecture automation.
- Strategic intelligence.
- Crowd monitoring.

Dù khác lĩnh vực, các giải pháp đều có điểm chung:

```text
Business problem
→ Data
→ AI reasoning
→ Tools hoặc services
→ Verification
→ User value
```

Điều này giúp tôi nhận ra rằng giá trị của AI không nằm riêng ở model, mà nằm ở cách model được đặt trong toàn bộ hệ thống.

### Hiểu rõ hơn về Agentic AI

Qua các phần trình bày, tôi hiểu Agentic AI không chỉ là chatbot trả lời tự nhiên. Một agent cần có:

- Goal.
- Context.
- Planning.
- Tools.
- State.
- Action.
- Verification.
- Guardrails.

Nếu thiếu các thành phần này, hệ thống có thể tạo ra câu trả lời hay nhưng chưa chắc thực hiện được công việc thật.

### Học cách cân bằng kỹ thuật và khả năng demo

Trong hackathon, nhóm không có đủ thời gian để xây dựng một hệ thống production hoàn chỉnh. Vì vậy cần lựa chọn đúng phần cốt lõi để chứng minh:

- Vấn đề có thật.
- Giải pháp có thể chạy.
- Kiến trúc có hướng mở rộng.
- Chi phí có thể giải thích.
- Demo thể hiện rõ giá trị.

### Học từ những thất bại nhỏ

Những câu chuyện như code không chạy, quên commit, thiếu phân công hoặc vô tình đẩy file môi trường lên repository cho thấy các sai sót vận hành có thể ảnh hưởng trực tiếp đến tiến độ.

Từ góc nhìn DevOps, đây là lời nhắc về tầm quan trọng của:

- Git discipline.
- Secret management.
- Automation.
- Ownership.
- Observability.
- Preparation.

---

## Bài Học Rút Ra

- Không cần chờ đến khi cảm thấy hoàn toàn sẵn sàng mới tham gia hackathon.
- Một nhóm có kỹ năng bổ sung cho nhau tốt hơn một nhóm có tất cả thành viên giống nhau.
- Nên thu nhỏ phạm vi và làm tốt một luồng chính.
- Kiến trúc cần phục vụ khả năng thay đổi của sản phẩm.
- AI phải được kết nối với dữ liệu và công cụ thật.
- Kết quả AI cần được xác minh trước khi tác động đến hệ thống thực tế.
- Chi phí và vận hành phải được xem xét ngay từ giai đoạn thiết kế.
- Một bản demo rõ ràng và ổn định quan trọng hơn việc cố nhồi nhiều tính năng.
- Những người gặp trong sự kiện và kinh nghiệm làm việc nhóm có giá trị không kém giải thưởng.

---

## Một Số Hình Ảnh Khi Tham Gia Sự Kiện

Do quá tập trung theo dõi các phần trình bày, lắng nghe những chia sẻ thực tế và trao đổi thêm với các nhóm cũng như mentor, em đã quên chụp lại hình ảnh trong buổi Capstone Presentation. Vì vậy, em không may không có hình ảnh kỷ niệm để lưu lại sau sự kiện.

Tuy nhiên, những kiến thức chuyên môn, kinh nghiệm triển khai thực tế và các góp ý từ mentor cùng các nhóm trình bày vẫn là những giá trị thiết thực nhất mà em thu nhận được. Đây cũng là bài học để em chuẩn bị tốt hơn cho những sự kiện sau, vừa chủ động ghi chép nội dung, vừa lưu lại một số hình ảnh quan trọng làm tư liệu và kỷ niệm.

> Tổng thể, sự kiện không chỉ giúp tôi tiếp cận thêm nhiều ứng dụng Agentic AI trên AWS mà còn cho thấy toàn bộ quá trình xây dựng sản phẩm: từ xác định vấn đề, thiết kế kiến trúc, phát triển MVP, kiểm soát chi phí đến chuẩn bị demo và làm việc nhóm. Đây là những kinh nghiệm có thể áp dụng trực tiếp vào quá trình học tập, thực tập và triển khai các dự án AWS sau này.
