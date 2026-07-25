+++
title = '5.1 Cognito'
weight = 1

[params]
  collapsibleMenu = true
+++

## Thiết lập xác thưc người dùng

### Sử dụng dịch vụ cognito

Cognito -> User Pool -> Create user pool

#### cài đặt

- Xác thực được sử dụng cho react nên thiết lập theo SPA ()
- Đặt tên cho ứng dụng xác thực

![Mô tả ảnh](/images/prj1.png)

- Thiết lập các yêu cầu khi đăng nhập

![Mô tả ảnh](/images/prj2.png)

- Đường dẫn sau khi đăng nhập thành công

![Mô tả ảnh](/images/prj3.png)

#### Những thông tin cần thiết để sử dụng cho việc code

Amazon Cognito -> User pools -> User pool - [id] -> Overview

Ta sẽ có User_pool_ID

Amazon Cognito -> User pools -> User pool - [id] -> App clients

Ta sẽ có Client ID