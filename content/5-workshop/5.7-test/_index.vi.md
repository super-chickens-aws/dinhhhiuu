+++
title = '5.7 Kiểm tra'
weight = 7

[params]
  collapsibleMenu = true
+++

## Kiểm tra ứng dụng

Sau khi hoàn tất việc triển khai, chúng ta tiến hành kiểm tra toàn bộ chức năng của hệ thống để đảm bảo ứng dụng hoạt động đúng như mong đợi.

---

## Truy cập ứng dụng

Đường dẫn ứng dụng sau khi triển khai thành công trên AWS Amplify:

```text
https://hieu.d1sl9gotr7i3f4.amplifyapp.com
```

### Giao diện trang chủ

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/prj26.png)

---

## Kiểm tra chức năng đăng ký và đăng nhập

### Bước 1. Đăng ký tài khoản

Thực hiện đăng ký tài khoản mới bằng địa chỉ email.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/prj27.png)

---

### Bước 2. Nhận mã xác thực

Sau khi đăng ký thành công, Amazon Cognito sẽ gửi mã xác thực về địa chỉ email đã đăng ký.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/prj28.png)

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/prj29.png)

---

### Bước 3. Xác thực tài khoản

Nhập mã xác thực để kích hoạt tài khoản.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/prj30.png)

---

### Bước 4. Đăng nhập

Sau khi xác thực thành công, người dùng có thể đăng nhập vào hệ thống.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/prj31.png)

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/prj32.png)

---

## Kiểm tra chức năng Text-to-Speech

Nhập nội dung văn bản, lựa chọn các tham số như giọng đọc, tốc độ, âm lượng và cao độ trước khi bắt đầu chuyển đổi.

### Nghe thử

Khi quá trình chuyển đổi thành công, hệ thống sẽ hiển thị trình phát âm thanh để người dùng có thể nghe thử trực tiếp.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/prj33.png)

---

### Tải file MP3

Nhấn **Download** để tải tệp âm thanh định dạng `.mp3`.

Đồng thời, hệ thống sẽ lưu lại lịch sử bao gồm nội dung văn bản và đường dẫn tới tệp âm thanh đã tạo.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/prj34.png)

---

## Kiểm tra chức năng Speech-to-Text

Chọn một tệp âm thanh `.mp3`, sau đó nhấn **Start Transcription**.

Nếu xử lý thành công, hệ thống sẽ trả về nội dung văn bản tương ứng với tệp âm thanh và tự động lưu kết quả vào lịch sử của người dùng.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/prj35.png)

---

## Kiểm tra lịch sử

Sau khi sử dụng các chức năng của hệ thống, người dùng có thể xem lại toàn bộ lịch sử chuyển đổi.

Lịch sử sẽ lưu đầy đủ thông tin văn bản và tệp âm thanh đã được tạo.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/prj36.png)

---

## Kết quả

Sau khi hoàn thành các bước kiểm tra, chúng ta có thể xác nhận rằng:

- Đăng ký và đăng nhập bằng Amazon Cognito hoạt động bình thường.
- Chức năng Text-to-Speech tạo tệp MP3 thành công.
- Chức năng Speech-to-Text trả về kết quả chính xác.
- Lịch sử chuyển đổi được lưu đầy đủ trong hệ thống.
- Người dùng có thể phát lại hoặc tải xuống các tệp âm thanh đã tạo.