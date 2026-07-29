+++
title = "1.4 Tuần 4 - Xây dựng Backend Serverless"
weight = 4

[params]
  collapsibleMenu = true
+++

## Mục tiêu

Trong tuần thứ tư, tôi bắt đầu xây dựng phần Backend cho dự án theo kiến trúc Serverless trên nền tảng AWS. Mục tiêu là tìm hiểu mô hình Serverless, triển khai các hàm AWS Lambda, xây dựng HTTP API bằng Amazon API Gateway và tạo nền tảng để các dịch vụ phía Frontend có thể giao tiếp với hệ thống.

---

## 4.1 Tìm hiểu kiến trúc Serverless

Trước khi bắt đầu phát triển Backend, tôi tìm hiểu mô hình **Serverless**.

Serverless là mô hình điện toán đám mây cho phép nhà phát triển tập trung xây dựng và triển khai chức năng của ứng dụng mà không cần quản lý máy chủ hay hạ tầng phía dưới. Việc cấp phát tài nguyên, mở rộng hệ thống và bảo trì máy chủ sẽ do nhà cung cấp dịch vụ Cloud đảm nhiệm.

Trong mô hình Serverless:

- AWS chịu trách nhiệm quản lý hạ tầng và máy chủ.
- Tài nguyên được tự động cấp phát khi có yêu cầu.
- Hệ thống có khả năng tự động mở rộng theo số lượng yêu cầu.
- Người dùng chỉ trả phí theo số lần thực thi và thời gian xử lý của hàm.

Để hiểu rõ hơn về mô hình này, tôi so sánh kiến trúc triển khai ứng dụng truyền thống với kiến trúc Serverless.

| Tiêu chí | Mô hình truyền thống (Traditional Server) | Mô hình Serverless |
|----------|--------------------------------------------|--------------------|
| Quản lý máy chủ | Người phát triển hoặc quản trị viên tự quản lý máy chủ | AWS quản lý toàn bộ hạ tầng |
| Triển khai ứng dụng | Cài đặt và cấu hình trên máy chủ | Chỉ cần triển khai mã nguồn của hàm |
| Khả năng mở rộng | Mở rộng thủ công hoặc cấu hình riêng | Tự động mở rộng theo lưu lượng truy cập |
| Chi phí | Trả phí theo thời gian máy chủ hoạt động | Trả phí theo số lần thực thi và thời gian xử lý |
| Bảo trì hệ thống | Tự cập nhật hệ điều hành, vá lỗi và bảo trì | AWS tự động thực hiện |
| Thời gian triển khai | Lâu hơn do cần chuẩn bị máy chủ | Nhanh, chỉ cần triển khai hàm |
| Phù hợp với | Hệ thống cần kiểm soát toàn bộ máy chủ hoặc chạy liên tục | API, Microservices, xử lý sự kiện, ứng dụng có lưu lượng thay đổi |

Qua nội dung này, tôi nhận thấy kiến trúc Serverless giúp giảm đáng kể khối lượng công việc liên quan đến quản lý hạ tầng, đồng thời tối ưu chi phí đối với các ứng dụng có lưu lượng truy cập không ổn định. Đây cũng là lý do tôi lựa chọn **AWS Lambda** để xây dựng Backend cho dự án trong quá trình thực tập.

---

## 4.2 Thiết kế kiến trúc Backend

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

---

## 4.3 Tạo AWS Lambda

Sau khi hoàn thiện thiết kế, tôi bắt đầu tạo hàm Lambda đầu tiên.

Các bước thực hiện: **Lambda → Create Function**

Sau đó cấu hình:

- Function Name
- Runtime (Node.js)
- Architecture
- Execution Role

Sau khi tạo thành công, AWS cung cấp giao diện để chỉnh sửa mã nguồn và triển khai trực tiếp.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog37.png)

---

## 4.4 Cấu hình IAM Role cho Lambda

Để Lambda có thể truy cập các dịch vụ AWS, tôi tiến hành cấu hình IAM Role.

Trong quá trình thực hành, tôi tìm hiểu:

- Execution Role
- Permission Policy
- Trust Relationship

Đồng thời cấp các quyền cần thiết để Lambda có thể hoạt động.

Ví dụ:

- CloudWatch Logs
- Amazon Polly 

Thêm quyền mới: **Role name → Add permissions → Attach Policies / Create inline policy**

Qua nội dung này, tôi hiểu rằng Lambda không sử dụng Access Key mà sử dụng IAM Role để xác thực với các dịch vụ AWS.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog38.png)

---

## 4.5 Viết mã nguồn Lambda

Sau khi tạo thành công hàm Lambda, tôi tiến hành xây dựng mã nguồn xử lý đầu tiên nhằm làm quen với cách Lambda nhận yêu cầu và trả kết quả.

Trong giai đoạn này, tôi xây dựng một hàm đơn giản có chức năng trả về thông điệp **"Hello from Lambda"**. Đây là bước kiểm thử cơ bản để xác nhận Lambda có thể thực thi thành công trước khi phát triển các chức năng phức tạp hơn.

Mã nguồn sử dụng:

```javascript
export const handler = async (event) => {
    return {
        statusCode: 200,
        headers: {
            "Content-Type": "application/json"
        },
        body: JSON.stringify({
            message: "Hello from Lambda"
        })
    };
};
```

### Giải thích mã nguồn

Đoạn chương trình trên gồm các thành phần chính:

| Thành phần | Chức năng |
|------------|-----------|
| `handler` | Hàm được AWS Lambda gọi khi có yêu cầu thực thi |
| `event` | Chứa dữ liệu gửi từ API Gateway hoặc dịch vụ AWS khác |
| `statusCode` | Mã trạng thái HTTP trả về cho Client |
| `headers` | Khai báo thông tin của dữ liệu trả về |
| `body` | Nội dung phản hồi, được chuyển thành chuỗi JSON |

Khi thực thi thành công, Lambda sẽ trả về kết quả:

```json
{
  "statusCode": 200,
  "headers": {
    "Content-Type": "application/json"
  },
  "body": "{\"message\":\"Hello from Lambda\"}"
}
```

Thông qua ví dụ này, tôi hiểu được cấu trúc cơ bản của một hàm AWS Lambda, cách Lambda trả dữ liệu theo chuẩn HTTP Response và cách API Gateway có thể nhận kết quả để gửi về cho ứng dụng Frontend.

---

# 4.6 Triển khai Lambda

Sau khi hoàn thiện mã nguồn, tôi tiến hành triển khai.

Các bước thực hiện:

- Chỉnh sửa mã nguồn.
- Nhấn **Deploy**.
- AWS cập nhật phiên bản mới của Lambda.

Sau khi triển khai thành công, hàm Lambda sẵn sàng để nhận yêu cầu từ API Gateway.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog39.png)

---

## 4.7 Kiểm thử Lambda

Sau khi hoàn thành mã nguồn, tôi tiến hành kiểm thử hàm Lambda bằng chức năng **Test** được tích hợp sẵn trên AWS Management Console.

Các bước thực hiện:

1. Mở trang chi tiết của hàm **AWS Lambda**.
2. Nhấn nút **Test** ở góc trên bên phải.
3. Lần đầu sử dụng, AWS yêu cầu tạo một **Test Event**.
4. Nhập tên cho Test Event (ví dụ: `test-event`).
5. Giữ nguyên dữ liệu mẫu mà AWS cung cấp.
6. Nhấn **Save**.
7. Tiếp tục nhấn **Test** để thực thi hàm.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog40.png)

---

### Kết quả thực thi

Sau khi kiểm thử thành công, AWS hiển thị các thông tin như:

- **Status:** Trạng thái thực thi (Succeeded hoặc Failed).
- **Response:** Kết quả trả về từ hàm Lambda.
- **Execution duration:** Thời gian thực thi.
- **Memory used:** Dung lượng bộ nhớ đã sử dụng.

Ví dụ kết quả:

```json
{
  "statusCode": 200,
  "headers": {
    "Content-Type": "application/json"
  },
  "body": "{\"message\":\"Hello from Lambda\"}"
}
```

Nếu hàm thực thi thành công, trạng thái sẽ hiển thị **Succeeded** và nội dung trả về đúng như đã lập trình.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog41.png)

---

### Kiểm tra Log thực thi

Sau mỗi lần chạy, AWS Lambda sẽ tự động ghi lại nhật ký thực thi (**Log**) vào **Amazon CloudWatch Logs**.

Nhờ đó, tôi có thể theo dõi quá trình thực thi của hàm, kiểm tra lỗi nếu có và hỗ trợ quá trình gỡ lỗi trong quá trình phát triển.

Thông qua việc kiểm thử trực tiếp trên AWS Console, tôi xác nhận hàm Lambda đã hoạt động đúng và sẵn sàng kết nối với Amazon API Gateway trong các bước tiếp theo.

---

## 4.8 Tìm hiểu Amazon API Gateway

Sau khi Lambda hoạt động ổn định, tôi tiếp tục tìm hiểu Amazon API Gateway.

API Gateway đóng vai trò tiếp nhận yêu cầu từ phía Frontend và chuyển tiếp tới Lambda.

Trong quá trình học, tôi tìm hiểu:

- HTTP API
- Route
- Stage
- Integration

Qua đó, tôi hiểu được vai trò của API Gateway trong kiến trúc Serverless.

---

## 4.9 Tạo HTTP API

Tôi tiến hành tạo HTTP API.

Các bước thực hiện: **API Gateway → Create API**

Chọn: **HTTP API**

Sau đó thực hiện:

- Đặt tên API.
- Chọn Integration là Lambda.
- Chọn Lambda Function vừa tạo.

Sau khi hoàn thành, API Gateway sinh ra Endpoint để Frontend có thể truy cập.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog42.png)

---

## 4.10 Tạo Route

Tiếp theo, tôi tạo các Route cho hệ thống.

Ví dụ:

- GET /
- POST /tts
- POST /hello

Mỗi Route được liên kết với một Lambda Function tương ứng.

Điều này giúp hệ thống dễ mở rộng khi số lượng API tăng lên.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog43.png)

---

## 4.11 Liên kết API Gateway với Lambda

Sau khi tạo Route, tôi cấu hình Integration giữa API Gateway và Lambda.

Quá trình này giúp:

- API Gateway nhận HTTP Request.
- Chuyển dữ liệu tới Lambda.
- Lambda xử lý.
- API Gateway trả kết quả về Frontend.

Đây là bước hoàn thiện luồng xử lý của Backend.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog44.png)

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

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog45.png)

---

## 4.13 Khó khăn gặp phải

Trong quá trình xây dựng Backend, tôi gặp một số khó khăn khi làm quen với mô hình Serverless, đặc biệt là cách Lambda nhận dữ liệu từ API Gateway và cách trả về kết quả theo đúng định dạng yêu cầu.

Ngoài ra, việc cấu hình IAM Role và liên kết Lambda với API Gateway cũng cần được kiểm tra cẩn thận để tránh lỗi phân quyền hoặc lỗi tích hợp.

---

## 4.14 Cách giải quyết

Để giải quyết các vấn đề trên, tôi tham khảo tài liệu chính thức của AWS, đọc log trên CloudWatch để xác định nguyên nhân lỗi và thực hiện kiểm thử sau mỗi lần thay đổi cấu hình.

Bên cạnh đó, tôi xây dựng từng API nhỏ trước khi mở rộng thêm các chức năng mới, giúp quá trình phát triển và kiểm thử trở nên dễ dàng hơn.

---

## 4.15 Kiến thức đạt được

Sau tuần thứ tư, tôi đã:

- Hiểu mô hình Serverless trên AWS.
- Thành thạo quy trình tạo và triển khai AWS Lambda.
- Biết cách cấu hình IAM Role cho Lambda.
- Hiểu cấu trúc của một HTTP API.
- Tạo và quản lý API bằng Amazon API Gateway.
- Liên kết API Gateway với Lambda.
- Kiểm thử và theo dõi quá trình thực thi thông qua CloudWatch Logs.

---

## 4.16 Đánh giá của bản thân

Tuần thứ tư đánh dấu bước chuyển từ việc học các dịch vụ AWS sang xây dựng Backend thực tế cho dự án. Việc trực tiếp triển khai AWS Lambda và Amazon API Gateway giúp tôi hiểu rõ hơn cách xây dựng một hệ thống Serverless và cách các thành phần trong kiến trúc phối hợp với nhau.

Đây là nền tảng quan trọng để trong các tuần tiếp theo tôi có thể tích hợp Amazon Cognito cho chức năng xác thực người dùng và Amazon Polly để xây dựng chức năng chuyển văn bản thành giọng nói cho ứng dụng.