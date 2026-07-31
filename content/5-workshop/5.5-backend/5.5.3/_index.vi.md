+++
title = '5.5.3 Create Lambda Function'
weight = 3

[params]
  collapsibleMenu = true
+++

## Tạo Lambda Function

Truy cập: **AWS Lambda** → **Functions** → **Create function**

Thiết lập các thông tin sau:

- **Function name**
- **Runtime**
- **Execution Role**

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog37.png)

Sau đó nhấn **Create function**.

---

## Cấp quyền cho Lambda

Mở Lambda vừa tạo và truy cập:

**Configuration** → **Permissions**

Chọn **Execution Role** để mở IAM Role của Lambda.

Trong IAM, cấp các quyền cần thiết để Lambda có thể làm việc với các dịch vụ AWS.

### Amazon Polly

Attach Policy: **AmazonPollyFullAccess**

---

### Amazon S3

Attach Policy: **AmazonS3FullAccess**

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/prj21.png)

---

### Amazon DynamoDB

Tạo **Inline Policy** hoặc Attach Policy phù hợp.

Cho phép các quyền:

- GetItem
- PutItem
- UpdateItem

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/prj22.png)

Chọn bảng: `SpeechHistory`

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/prj23.png)

Nhấn **Next**.

Đặt tên Policy: `dynamoSpeechHistory`

Sau đó nhấn **Create Policy** để hoàn thành.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/prj24.png)

---

## Thiết lập Bucket Policy

Để frontend có thể tải file MP3 từ S3, cấu hình **Bucket Policy** cho Bucket.

Truy cập: **Amazon S3** → **Bucket** → **\<Bucket Name\>** → **Permissions** → **Bucket Policy**

Dán Policy sau để cho phép tải xuống từ S3:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicRead",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::voice-ai-media-superchicken/*"
    }
  ]
}
```

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/prj25.png)

---

## Triển khai mã nguồn

Tải mã nguồn Lambda tại:

**GitHub Repository**

https://github.com/super-chickens-aws/polly-voice/tree/main/backend

Cài đặt các thư viện:

```bash
npm install
```

Sau đó nén toàn bộ mã nguồn thành một file `.zip`.

Trong quá trình xử lý, Lambda sẽ:

- Nhận yêu cầu từ API Gateway.
- Gọi Amazon Polly để tạo giọng nói.
- Lưu file MP3 lên Amazon S3.
- Ghi lịch sử vào DynamoDB.
- Trả kết quả về frontend.

---

## Deploy và Test

Trong trang Lambda:

- Chọn **Update**
- Chọn **Upload from**
- Chọn **.zip file**
- Tải lên file `.zip` đã tạo ở bước trước

Sau khi cập nhật mã nguồn:

- Nhấn **Deploy**
- Tạo **Test Event**
- Chạy **Test**

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog39.png)

Nếu thực hiện thành công, Lambda sẽ:

- Sinh file MP3.
- Upload lên Amazon S3.
- Lưu dữ liệu vào DynamoDB.
- Trả về kết quả thành công.