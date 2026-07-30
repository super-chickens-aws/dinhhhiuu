+++
title = '2. Bản đề xuất'
weight = 2

[params]
  collapsibleMenu = true
+++

## Polly Voice
Ứng dụng chuyển văn bản thành giọng nói sử dụng AWS Serverless

---

## 1. Tổng quan dự án

### Mục tiêu

Polly Voice là một ứng dụng web được xây dựng nhằm chuyển đổi văn bản thành giọng nói (Text-to-Speech) bằng dịch vụ Amazon Polly. Người dùng có thể đăng nhập vào hệ thống, nhập nội dung văn bản, lựa chọn giọng đọc phù hợp và tạo ra tệp âm thanh chất lượng cao để nghe trực tiếp hoặc tải xuống.

Ứng dụng được phát triển hoàn toàn theo kiến trúc Serverless trên nền tảng Amazon Web Services (AWS), giúp giảm chi phí vận hành, dễ dàng mở rộng và không cần quản lý máy chủ.

---

## 2. Vấn đề cần giải quyết

### Thực trạng

Hiện nay nhiều người có nhu cầu chuyển đổi văn bản thành giọng nói phục vụ học tập, đọc tài liệu, tạo nội dung hoặc hỗ trợ người khiếm thị. Tuy nhiên:

- Nhiều dịch vụ Text-to-Speech yêu cầu trả phí.
- Một số nền tảng không hỗ trợ đầy đủ nhiều ngôn ngữ.
- Việc xây dựng hệ thống TTS truyền thống cần triển khai và quản lý máy chủ, gây tốn thời gian và chi phí.

### Giải pháp

Polly Voice sử dụng Amazon Polly để thực hiện việc tổng hợp giọng nói chất lượng cao. Hệ thống áp dụng kiến trúc Serverless gồm:

- Amazon Cognito quản lý người dùng.
- React chạy trên AWS Amplify.
- API Gateway tiếp nhận yêu cầu từ frontend.
- AWS Lambda xử lý nghiệp vụ.
- Amazon Polly sinh file âm thanh.
- Amazon S3 lưu trữ file mp3.
- Amazon DynamoDB lưu lịch sử chuyển đổi.

Người dùng chỉ cần đăng nhập, nhập văn bản, chọn giọng đọc và hệ thống sẽ tự động tạo file âm thanh.

### Lợi ích

- Không cần quản lý server.
- Chi phí vận hành thấp.
- Dễ dàng mở rộng khi số lượng người dùng tăng.
- Tốc độ xử lý nhanh.
- Có thể tái sử dụng cho nhiều ứng dụng AI hoặc học tập trong tương lai.

---

## 3. Kiến trúc giải pháp

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog53.png)

### Dịch vụ AWS sử dụng

- AWS Amplify: Triển khai giao diện React.
- Amazon Cognito: Đăng ký và đăng nhập người dùng.
- Amazon API Gateway: Cung cấp REST API.
- AWS Lambda: Xử lý nghiệp vụ.
- Amazon Polly: Chuyển văn bản thành giọng nói.
- Amazon S3: Lưu file âm thanh.
- Amazon DynamoDB: Lưu lịch sử tạo giọng nói.

### Luồng hoạt động

1. Người dùng đăng nhập bằng Cognito.
2. Frontend gửi yêu cầu tới API Gateway.
3. API Gateway gọi Lambda.
4. Lambda gọi Amazon Polly để tạo giọng nói.
5. File mp3 được lưu vào Amazon S3.
6. Lambda lưu thông tin lịch sử vào DynamoDB.
7. URL file âm thanh được trả về frontend.
8. Người dùng có thể nghe hoặc tải xuống.

---

## 4. Timeline

### Giai đoạn 1

- Nghiên cứu Amazon Polly.
- Tìm hiểu kiến trúc Serverless.
- Thiết kế hệ thống.

### Giai đoạn 2

- Xây dựng Backend.
- Tạo Lambda.
- Tích hợp API Gateway.
- Kết nối Amazon Polly.
- Lưu file vào Amazon S3.

### Giai đoạn 3

- Xây dựng giao diện React.
- Tích hợp Cognito.
- Kết nối Backend.

### Giai đoạn 4

- Kiểm thử.
- Hoàn thiện giao diện.
- Triển khai lên AWS Amplify.

---

## 5. Ngân sách

Ứng dụng sử dụng các dịch vụ thuộc AWS Free Tier trong quá trình phát triển.

Ước tính chi phí khi triển khai ở quy mô nhỏ:

| Dịch vụ | Chi phí/tháng |
|----------|---------------|
| Amazon Polly | ~0.20 USD |
| AWS Lambda | ~0.00 USD |
| API Gateway | ~0.01 USD |
| Amazon S3 | ~0.05 USD |
| DynamoDB | ~0.02 USD |
| AWS Amplify | ~0.10 USD |
| Amazon Cognito | ~0.00 USD |

**Tổng chi phí ước tính:** khoảng **0.38 USD/tháng**.

---

## 6. Rủi ro

### Các rủi ro

- Người dùng nhập văn bản vượt giới hạn.
- Giới hạn Free Tier của Amazon Polly.
- File âm thanh lưu trữ quá nhiều làm tăng chi phí S3.
- Lỗi xác thực người dùng.

### Giải pháp

- Giới hạn số ký tự cho mỗi lần chuyển đổi.
- Thiết lập IAM theo nguyên tắc Least Privilege.
- Xóa hoặc lưu trữ định kỳ các file cũ.
- Sử dụng Cognito JWT để xác thực mọi API.

---

## 7. Kết quả kỳ vọng

Sau khi hoàn thành, hệ thống sẽ:

- Cho phép người dùng đăng ký và đăng nhập.
- Chuyển đổi văn bản thành giọng nói bằng Amazon Polly.
- Phát và tải file mp3.
- Lưu lịch sử chuyển đổi.
- Triển khai hoàn toàn trên nền tảng AWS Serverless.
- Có thể mở rộng thêm nhiều ngôn ngữ, nhiều giọng đọc và tích hợp các dịch vụ AI khác trong tương lai.