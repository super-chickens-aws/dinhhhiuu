+++
title = "1.6 Tuần 6 - Xây dựng chức năng Text-to-Speech"
weight = 6

[params]
  collapsibleMenu = true
+++

# Tuần 6 - Xây dựng chức năng Text-to-Speech

## Mục tiêu

Trong tuần thứ sáu, tôi tập trung phát triển chức năng chính của dự án là chuyển đổi văn bản thành giọng nói (Text-to-Speech). Mục tiêu là tích hợp dịch vụ Amazon Polly vào hệ thống Backend Serverless, xây dựng API xử lý yêu cầu từ người dùng và trả về kết quả là tệp âm thanh được tổng hợp bằng trí tuệ nhân tạo.

---

# 6.1 Tìm hiểu Amazon Polly

Trước khi bắt đầu phát triển chức năng, tôi tìm hiểu dịch vụ Amazon Polly.

Amazon Polly là dịch vụ AI của AWS có khả năng chuyển đổi văn bản thành giọng nói tự nhiên bằng công nghệ tổng hợp giọng nói (Text-to-Speech).

Trong quá trình tìm hiểu, tôi nghiên cứu các nội dung:

- Các ngôn ngữ được hỗ trợ.
- Các giọng đọc (Voice).
- Các Engine tổng hợp giọng nói.
- Các định dạng âm thanh đầu ra.
- Các API do AWS SDK cung cấp.

Qua đó, tôi hiểu được quy trình Amazon Polly tiếp nhận văn bản, xử lý và sinh ra dữ liệu âm thanh.

> **Chèn hình:** Tổng quan Amazon Polly.

---

# 6.2 Thiết kế chức năng Text-to-Speech

Sau khi tìm hiểu Amazon Polly, tôi tiến hành thiết kế chức năng Text-to-Speech cho dự án.

Luồng xử lý được xây dựng như sau:

```text
Người dùng
      │
      ▼
Frontend (React)
      │
HTTP Request
      │
      ▼
API Gateway
      │
      ▼
AWS Lambda
      │
AWS SDK
      │
      ▼
Amazon Polly
      │
Audio Stream
      │
      ▼
Frontend
```

Với kiến trúc này, toàn bộ quá trình xử lý được thực hiện trên nền tảng Serverless.

> **Chèn hình:** Kiến trúc Text-to-Speech.

---

# 6.3 Cấu hình quyền truy cập Amazon Polly

Để AWS Lambda có thể gọi Amazon Polly, tôi tiến hành cấu hình IAM Role.

Các bước thực hiện:

IAM → Roles

Sau đó cấp quyền:

- AmazonPollyFullAccess

hoặc Policy chỉ cho phép:

- polly:SynthesizeSpeech

Sau khi hoàn thành, Lambda đã có quyền sử dụng Amazon Polly.

> **Chèn hình:** IAM Role.

---

# 6.4 Tích hợp AWS SDK vào Lambda

Tiếp theo, tôi tích hợp AWS SDK vào dự án Backend.

Các nội dung thực hiện:

- Cài đặt AWS SDK.
- Khởi tạo Polly Client.
- Cấu hình Region.
- Khởi tạo yêu cầu gửi tới Amazon Polly.

Thông qua nội dung này, Lambda có thể giao tiếp trực tiếp với dịch vụ Amazon Polly.

> **Chèn hình:** Cấu hình AWS SDK.

---

# 6.5 Xây dựng API Text-to-Speech

Sau khi hoàn thành phần kết nối, tôi tiến hành xây dựng API chuyển văn bản thành giọng nói.

API tiếp nhận dữ liệu từ Frontend dưới dạng JSON.

Ví dụ:

```json
{
    "text": "Xin chào AWS",
    "voice": "Linh",
    "engine": "neural"
}
```

Sau khi nhận dữ liệu, Lambda thực hiện:

- Kiểm tra dữ liệu đầu vào.
- Gửi yêu cầu tới Amazon Polly.
- Nhận dữ liệu âm thanh.
- Trả kết quả về cho Frontend.

Thông qua quá trình này, tôi hoàn thành chức năng cốt lõi của Backend.

> **Chèn hình:** API `/tts`.

---

# 6.6 Thiết lập các tham số tổng hợp giọng nói

Để người dùng có thể lựa chọn giọng đọc phù hợp, tôi nghiên cứu và cấu hình các tham số của Amazon Polly.

Các tham số sử dụng gồm:

- Voice ID
- Engine
- Output Format
- Language

Ngoài ra, tôi tìm hiểu sự khác nhau giữa các Engine tổng hợp giọng nói và lựa chọn Engine phù hợp cho ứng dụng.

Qua đó, chức năng Text-to-Speech có thể đáp ứng nhiều nhu cầu sử dụng khác nhau.

> **Chèn hình:** Danh sách Voice.

---

# 6.7 Xử lý dữ liệu âm thanh

Sau khi Amazon Polly tổng hợp giọng nói, Lambda nhận về dữ liệu âm thanh dưới dạng luồng dữ liệu (Audio Stream).

Tôi thực hiện:

- Chuyển đổi dữ liệu về định dạng phù hợp.
- Thiết lập Content-Type.
- Trả dữ liệu về Frontend thông qua API Gateway.

Sau khi hoàn thành, Frontend có thể phát trực tiếp hoặc tải xuống tệp âm thanh.

> **Chèn hình:** Response Audio.

---

# 6.8 Kiểm thử chức năng

Sau khi hoàn thành chức năng, tôi tiến hành kiểm thử.

Các nội dung kiểm thử gồm:

- Văn bản ngắn.
- Văn bản dài.
- Nội dung tiếng Việt.
- Nội dung tiếng Anh.
- Nhiều Voice khác nhau.
- Các Engine khác nhau.

Ngoài ra, tôi kiểm tra các trường hợp:

- Văn bản rỗng.
- Văn bản vượt quá giới hạn.
- Voice không tồn tại.

Kết quả cho thấy API hoạt động đúng theo yêu cầu thiết kế.

> **Chèn hình:** Kết quả kiểm thử.

---

# 6.9 Tối ưu xử lý

Sau khi chức năng hoạt động ổn định, tôi tiến hành tối ưu mã nguồn.

Các nội dung thực hiện:

- Chuẩn hóa cấu trúc mã nguồn.
- Tách Business Logic khỏi Handler.
- Bổ sung xử lý ngoại lệ.
- Chuẩn hóa định dạng Response.
- Bổ sung ghi log phục vụ kiểm thử.

Việc tối ưu giúp mã nguồn dễ bảo trì và thuận tiện cho việc mở rộng các chức năng trong tương lai.

---

# 6.10 Khó khăn gặp phải

Trong quá trình tích hợp Amazon Polly, tôi gặp một số khó khăn khi xử lý dữ liệu âm thanh trả về từ dịch vụ cũng như việc cấu hình quyền truy cập giữa AWS Lambda và Amazon Polly.

Bên cạnh đó, việc xử lý các trường hợp dữ liệu đầu vào không hợp lệ và đảm bảo API luôn trả về kết quả đúng định dạng cũng cần được kiểm tra cẩn thận.

---

# 6.11 Cách giải quyết

Để giải quyết các vấn đề trên, tôi tham khảo tài liệu chính thức của AWS, kiểm tra log trên CloudWatch và thực hiện nhiều lần kiểm thử với các loại dữ liệu đầu vào khác nhau.

Ngoài ra, tôi tách riêng phần xử lý nghiệp vụ khỏi phần tiếp nhận yêu cầu của Lambda, giúp mã nguồn rõ ràng hơn và thuận tiện trong quá trình bảo trì.

---

# 6.12 Kiến thức đạt được

Sau tuần thứ sáu, tôi đã:

- Hiểu nguyên lý hoạt động của Amazon Polly.
- Biết cách sử dụng AWS SDK để gọi dịch vụ AWS.
- Tích hợp thành công Amazon Polly với AWS Lambda.
- Xây dựng API chuyển văn bản thành giọng nói.
- Biết cách xử lý dữ liệu âm thanh trả về từ Amazon Polly.
- Hiểu luồng xử lý giữa Frontend, API Gateway, Lambda và Amazon Polly.
- Hoàn thiện chức năng cốt lõi của dự án.

---

# 6.13 Đánh giá của bản thân

Tuần thứ sáu là giai đoạn quan trọng nhất trong quá trình phát triển dự án vì chức năng chính của ứng dụng đã được hoàn thiện. Việc tích hợp thành công Amazon Polly với kiến trúc Serverless giúp tôi hiểu rõ hơn cách kết hợp các dịch vụ AI của AWS để xây dựng ứng dụng thực tế.

Sau khi hoàn thành tuần này, hệ thống đã có khả năng tiếp nhận văn bản từ người dùng, chuyển đổi thành giọng nói và trả kết quả thông qua API. Đây là nền tảng để trong tuần tiếp theo tôi tiếp tục xây dựng giao diện người dùng, tích hợp Frontend với Backend và triển khai ứng dụng lên Internet bằng AWS Amplify.