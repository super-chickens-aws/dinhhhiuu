+++
title = '5.1 Cognito'
weight = 1

[params]
  collapsibleMenu = true
+++

## Thiết lập xác thực người dùng

### Sử dụng dịch vụ Cognito

Truy cập:

**Amazon Cognito** → **User pools** → **Create user pool**

### Cài đặt

Thiết lập các thông tin cơ bản:

- Ứng dụng xác thực sử dụng **React**, vì vậy chọn loại ứng dụng **SPA (Single Page Application)**.
- Đặt tên cho ứng dụng xác thực.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/prj1.png)

Thiết lập các yêu cầu khi đăng nhập.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/prj2.png)

Thiết lập đường dẫn chuyển hướng sau khi đăng nhập thành công.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/prj3.png)

Sau khi hoàn tất, nhấn **Create user pool** để tạo User Pool.

---

## Những thông tin cần thiết để sử dụng khi lập trình

Để kết nối ứng dụng với Amazon Cognito, cần lấy các thông tin sau.

### User Pool ID

Truy cập:

**Amazon Cognito** → **User pools** → **User pool - [id]** → **Overview**

Tại đây sẽ có:

- **User Pool ID**

### Client ID

Truy cập:

**Amazon Cognito** → **User pools** → **User pool - [id]** → **App clients**

Tại đây sẽ có:

- **Client ID**