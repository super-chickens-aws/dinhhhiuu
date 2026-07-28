+++
title = "1.4 Tuần 4 - Xây dựng Backend Serverless"
weight = 4

[params]
  collapsibleMenu = true
+++

# Tuần 4 - Xây dựng Backend Serverless

## Mục tiêu

Trong tuần thứ tư, tôi bắt đầu xây dựng phần Backend cho dự án theo kiến trúc Serverless trên nền tảng AWS. Mục tiêu là tìm hiểu mô hình Serverless, triển khai các hàm AWS Lambda, xây dựng HTTP API bằng Amazon API Gateway và tạo nền tảng để các dịch vụ phía Frontend có thể giao tiếp với hệ thống.

---

# 4.1 Tìm hiểu kiến trúc Serverless

Trước khi bắt đầu phát triển Backend, tôi tìm hiểu mô hình Serverless.

Serverless là mô hình điện toán cho phép nhà phát triển chỉ tập trung vào việc xây dựng chức năng của ứng dụng mà không cần quản lý máy chủ.

Trong mô hình này:

- AWS chịu trách nhiệm quản lý hạ tầng.
- Tài nguyên được cấp phát tự động khi có yêu cầu.
- Chỉ tính phí theo số lần thực thi và thời gian xử lý.

Tôi cũng tìm hiểu sự khác nhau giữa mô hình truyền thống sử dụng máy chủ và kiến trúc Serverless.

Qua nội dung này, tôi hiểu được lý do AWS Lambda phù hợp với các ứng dụng có quy mô nhỏ và trung bình, đồng thời giúp giảm chi phí vận hành.

> **Chèn hình:** So sánh Traditional Server và Serverless.

---

# 4.2 Thiết kế kiến trúc Backend

Trước khi viết mã nguồn, tôi tiến hành thiết kế kiến trúc tổng thể của Backend.

Hệ thống được xây dựng gồm các thành phần:

- React Frontend
- Amazon API Gateway
- AWS Lambda
- Amazon Polly (ở các tuần tiếp theo)

Luồng xử lý được thiết kế như sau:

```
Frontend
      │
      ▼
API Gateway
      │
      ▼
Lambda
      │
      ▼
Business Logic
```

Kiến trúc này giúp Frontend chỉ cần gọi HTTP API mà không cần biết cách Backend được triển khai.

> **Chèn hình:** Kiến trúc Backend Serverless.

---

# 4.3 Tạo AWS Lambda

Sau khi hoàn thiện thiết kế, tôi bắt đầu tạo hàm Lambda đầu tiên.

Các bước thực hiện:

Lambda → Create Function

Sau đó cấu hình:

- Function Name
- Runtime (Node.js)
- Architecture
- Execution Role

Sau khi tạo thành công, AWS cung cấp giao diện để chỉnh sửa mã nguồn và triển khai trực tiếp.

> **Chèn hình:** Create Lambda Function.

---

# 4.4 Cấu hình IAM Role cho Lambda

Để Lambda có thể truy cập các dịch vụ AWS, tôi tiến hành cấu hình IAM Role.

Trong quá trình thực hành, tôi tìm hiểu:

- Execution Role
- Permission Policy
- Trust Relationship

Đồng thời cấp các quyền cần thiết để Lambda có thể hoạt động.

Ví dụ:

- CloudWatch Logs
- Amazon Polly (sử dụng ở các tuần sau)

Qua nội dung này, tôi hiểu rằng Lambda không sử dụng Access Key mà sử dụng IAM Role để xác thực với các dịch vụ AWS.

> **Chèn hình:** IAM Role của Lambda.

---

# 4.5 Viết mã nguồn Lambda

Sau khi tạo Lambda, tôi bắt đầu xây dựng mã nguồn xử lý.

Các nội dung thực hiện gồm:

- Nhận dữ liệu từ API Gateway.
- Xử lý dữ liệu đầu vào.
- Trả kết quả theo định dạng JSON.
- Xử lý ngoại lệ khi có lỗi xảy ra.

Ví dụ kết quả trả về:

```json
{
  "statusCode": 200,
  "body": "Hello from Lambda"
}
```

Thông qua quá trình này, tôi hiểu được cấu trúc cơ bản của một hàm Lambda và cách Lambda giao tiếp với API Gateway.

> **Chèn hình:** Mã nguồn Lambda.

---

# 4.6 Triển khai Lambda

Sau khi hoàn thiện mã nguồn, tôi tiến hành triển khai.

Các bước thực hiện:

- Chỉnh sửa mã nguồn.
- Nhấn **Deploy**.
- AWS cập nhật phiên bản mới của Lambda.

Sau khi triển khai thành công, hàm Lambda sẵn sàng để nhận yêu cầu từ API Gateway.

> **Chèn hình:** Deploy Lambda.

---

# 4.7 Kiểm thử Lambda

Để kiểm tra hoạt động của Lambda, tôi sử dụng chức năng Test.

Các bước thực hiện:

- Tạo Test Event.
- Nhập dữ liệu mẫu.
- Thực hiện Test.

Sau khi chạy thành công, AWS hiển thị:

- Response
- Execution Time
- Log Output

Thông qua CloudWatch Logs, tôi có thể kiểm tra chi tiết quá trình thực thi của Lambda.

> **Chèn hình:** Test Lambda.

---

# 4.8 Tìm hiểu Amazon API Gateway

Sau khi Lambda hoạt động ổn định, tôi tiếp tục tìm hiểu Amazon API Gateway.

API Gateway đóng vai trò tiếp nhận yêu cầu từ phía Frontend và chuyển tiếp tới Lambda.

Trong quá trình học, tôi tìm hiểu:

- HTTP API
- Route
- Stage
- Integration

Qua đó, tôi hiểu được vai trò của API Gateway trong kiến trúc Serverless.

> **Chèn hình:** Amazon API Gateway.

---

# 4.9 Tạo HTTP API

Tôi tiến hành tạo HTTP API.

Các bước thực hiện:

API Gateway → Create API

Chọn:

- HTTP API

Sau đó thực hiện:

- Đặt tên API.
- Chọn Integration là Lambda.
- Chọn Lambda Function vừa tạo.

Sau khi hoàn thành, API Gateway sinh ra Endpoint để Frontend có thể truy cập.

> **Chèn hình:** Create HTTP API.

---

# 4.10 Tạo Route

Tiếp theo, tôi tạo các Route cho hệ thống.

Ví dụ:

- GET /
- POST /tts
- POST /hello

Mỗi Route được liên kết với một Lambda Function tương ứng.

Điều này giúp hệ thống dễ mở rộng khi số lượng API tăng lên.

> **Chèn hình:** Routes.

---

# 4.11 Liên kết API Gateway với Lambda

Sau khi tạo Route, tôi cấu hình Integration giữa API Gateway và Lambda.

Quá trình này giúp:

- API Gateway nhận HTTP Request.
- Chuyển dữ liệu tới Lambda.
- Lambda xử lý.
- API Gateway trả kết quả về Frontend.

Đây là bước hoàn thiện luồng xử lý của Backend.

> **Chèn hình:** Lambda Integration.

---

# 4.12 Kiểm thử API

Sau khi hoàn thiện Backend, tôi tiến hành kiểm thử API.

Các công cụ sử dụng:

- Trình duyệt Web.
- Postman.
- Thunder Client (Visual Studio Code).

Tôi kiểm tra:

- HTTP Status Code.
- Response Body.
- Response Time.
- Các trường hợp lỗi.

Sau khi kiểm thử, các API đều hoạt động đúng theo thiết kế.

> **Chèn hình:** Kết quả kiểm thử API.

---

# 4.13 Khó khăn gặp phải

Trong quá trình xây dựng Backend, tôi gặp một số khó khăn khi làm quen với mô hình Serverless, đặc biệt là cách Lambda nhận dữ liệu từ API Gateway và cách trả về kết quả theo đúng định dạng yêu cầu.

Ngoài ra, việc cấu hình IAM Role và liên kết Lambda với API Gateway cũng cần được kiểm tra cẩn thận để tránh lỗi phân quyền hoặc lỗi tích hợp.

---

# 4.14 Cách giải quyết

Để giải quyết các vấn đề trên, tôi tham khảo tài liệu chính thức của AWS, đọc log trên CloudWatch để xác định nguyên nhân lỗi và thực hiện kiểm thử sau mỗi lần thay đổi cấu hình.

Bên cạnh đó, tôi xây dựng từng API nhỏ trước khi mở rộng thêm các chức năng mới, giúp quá trình phát triển và kiểm thử trở nên dễ dàng hơn.

---

# 4.15 Kiến thức đạt được

Sau tuần thứ tư, tôi đã:

- Hiểu mô hình Serverless trên AWS.
- Thành thạo quy trình tạo và triển khai AWS Lambda.
- Biết cách cấu hình IAM Role cho Lambda.
- Hiểu cấu trúc của một HTTP API.
- Tạo và quản lý API bằng Amazon API Gateway.
- Liên kết API Gateway với Lambda.
- Kiểm thử và theo dõi quá trình thực thi thông qua CloudWatch Logs.

---

# 4.16 Đánh giá của bản thân

Tuần thứ tư đánh dấu bước chuyển từ việc học các dịch vụ AWS sang xây dựng Backend thực tế cho dự án. Việc trực tiếp triển khai AWS Lambda và Amazon API Gateway giúp tôi hiểu rõ hơn cách xây dựng một hệ thống Serverless và cách các thành phần trong kiến trúc phối hợp với nhau.

Đây là nền tảng quan trọng để trong các tuần tiếp theo tôi có thể tích hợp Amazon Cognito cho chức năng xác thực người dùng và Amazon Polly để xây dựng chức năng chuyển văn bản thành giọng nói cho ứng dụng.