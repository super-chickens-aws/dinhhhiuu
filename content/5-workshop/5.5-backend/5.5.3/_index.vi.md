+++
title = '5.5.3 Create Lambda Function'
weight = 3

[params]
  collapsibleMenu = true
+++

## Tạo Lambda Function

Truy cập: **AWS Lambda** → **Functions** → **Create function**

Thiết lập:

- Function name
- Runtime
- Execution Role

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog37.png)

Sau đó nhấn **Create function**.

---

## Cấp quyền cho Lambda

Mở Lambda vừa tạo.

Truy cập: **Configuration** → **Permissions**

Chọn **Execution Role**.

Trong IAM, cấp các quyền cần thiết để Lambda có thể làm việc với các dịch vụ AWS.

### Amazon Polly

Attach Policy: **AmazonPollyFullAccess**

---

### Amazon S3

Attach Policy: **AmazonS3FullAccess**

---

### Amazon DynamoDB

Tạo **Inline Policy** hoặc Attach Policy phù hợp.

Cho phép các quyền:

- GetItem
- PutItem
- UpdateItem

Đối tượng truy cập:

- Bảng `SpeechHistory`

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog38.png)

---

## Thiết lập Bucket Policy

Để frontend có thể tải file MP3 từ S3, cấu hình **Bucket Policy** cho Bucket.

Truy cập: **S3** → **Bucket** → **Permissions** → **Bucket Policy**

Thêm Bucket Policy phù hợp.

> **Screenshot:** Bucket Policy

---

## Triển khai mã nguồn

Tải mã nguồn Lambda lên và cấu hình các thông số cần thiết.

Trong quá trình xử lý, Lambda sẽ:

- Nhận yêu cầu từ API Gateway.
- Gọi Amazon Polly để tạo giọng nói.
- Lưu file MP3 lên Amazon S3.
- Ghi lịch sử vào DynamoDB.
- Trả kết quả về frontend.

---

## Deploy và Test

Sau khi hoàn thành mã nguồn:

- Nhấn **Deploy**
- Tạo **Test Event**
- Chạy **Test**

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog39.png)

Nếu thực hiện thành công, Lambda sẽ:

- Sinh file MP3.
- Upload lên S3.
- Lưu dữ liệu vào DynamoDB.
- Trả về kết quả thành công.