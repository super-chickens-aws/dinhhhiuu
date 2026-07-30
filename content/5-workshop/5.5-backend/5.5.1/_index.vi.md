+++
title = '5.5.1 Create DynamoDB Tables'
weight = 1

[params]
  collapsibleMenu = true
+++

## Giới thiệu

Trong phần này, chúng ta sẽ tạo các bảng **Amazon DynamoDB** để lưu trữ dữ liệu của ứng dụng Polly Voice.

Ứng dụng sử dụng hai bảng DynamoDB:

- **Users**: Lưu thông tin người dùng.
- **SpeechHistory**: Lưu lịch sử các lần chuyển đổi văn bản thành giọng nói.

---

## Tạo bảng Users

Truy cập: **Amazon DynamoDB** → **Tables** → **Create table**

Cấu hình bảng với các thông tin sau:

- **Table name:** `Users`
- **Partition key:** `userId`

Các thiết lập còn lại giữ mặc định, sau đó nhấn **Create table**.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/prj13.png)

---

## Tạo bảng SpeechHistory

Tiếp tục chọn **Create table** để tạo bảng lưu lịch sử chuyển đổi.

Cấu hình như sau:

- **Table name:** `SpeechHistory`
- **Partition key:** `userId`
- **Sort key:** `createdAt`

Các thiết lập còn lại giữ mặc định và nhấn **Create table**.

> **Screenshot:** Create SpeechHistory Table

---

## Cấu trúc dữ liệu

Mỗi bản ghi trong bảng **SpeechHistory** sẽ lưu thông tin của một lần chuyển đổi, bao gồm:

- **userId**: Định danh người dùng.
- **createdAt**: Thời điểm tạo bản ghi.
- **text**: Nội dung văn bản được chuyển đổi.
- **voiceId**: Giọng đọc được sử dụng.
- **engine**: Loại engine của Amazon Polly.
- **speed**: Tốc độ đọc.
- **pitch**: Cao độ giọng đọc.
- **volume**: Âm lượng.
- **audioKey**: Đường dẫn tệp MP3 trên Amazon S3.

Ví dụ:

```json
{
  "userId": "abc123",
  "createdAt": "2026-07-27T16:20:10Z",
  "text": "Hello AWS",
  "voiceId": "Danielle",
  "engine": "neural",
  "speed": 100,
  "pitch": 0,
  "volume": 100,
  "audioKey": "tts/1785082534512.mp3"
}
```

---

## Kết quả

Sau khi hoàn thành, chúng ta sẽ có hai bảng DynamoDB:

- **Users**: Lưu thông tin tài khoản người dùng.
- **SpeechHistory**: Lưu lịch sử chuyển đổi văn bản thành giọng nói.

Hai bảng này sẽ được AWS Lambda sử dụng để quản lý dữ liệu của ứng dụng trong các bước tiếp theo.

<!-- ## Cấp quyền cho Lambda  

Hiện lambda chưa có quyền truy cập DynamoDB nên chúng ta phải dùng IAM Role để cấp

Lambda -> Function -> voice-ai-api -> Configuration -> Permissions

Execution role -> Role name

Trong IAM -> Add permissions -> Create inline policy

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/prj14.png)

Actions cấp 3 quyền: GetItem, PutItem, UpdateItem

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/prj15.png)

Đặt tên cho policy

Ấn **Create** để hoàn thành -->