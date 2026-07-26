+++
title = "1.5 Tuần 5 - Xác thực người dùng với Amazon Cognito"
weight = 5

[params]
  collapsibleMenu = true
+++

## Mục tiêu

- Tìm hiểu dịch vụ Amazon Cognito.
- Xây dựng chức năng đăng ký và đăng nhập người dùng.
- Bảo vệ API bằng cơ chế xác thực JWT.
- Tích hợp Cognito vào ứng dụng.

---

## Nội dung thực hiện

Trong tuần thứ năm, tôi nghiên cứu dịch vụ Amazon Cognito để xây dựng hệ thống xác thực người dùng cho ứng dụng.

Tôi tìm hiểu cách tạo User Pool, App Client và cấu hình các phương thức đăng nhập phù hợp với ứng dụng React.

Sau khi hoàn thành cấu hình Cognito, tôi tiếp tục tích hợp cơ chế xác thực vào Amazon API Gateway thông qua JWT Authorizer nhằm đảm bảo chỉ những người dùng đã đăng nhập mới có thể sử dụng các API được bảo vệ.

Các công việc đã thực hiện gồm:

- Tạo Amazon Cognito User Pool.
- Cấu hình App Client.
- Thiết lập Redirect URI.
- Tích hợp Cognito với ứng dụng React.
- Cấu hình JWT Authorizer trong API Gateway.
- Kiểm thử quá trình đăng nhập và xác thực.

---

## Kiến thức đạt được

Sau tuần thứ năm, tôi hiểu được:

- Quy trình xác thực người dùng bằng Amazon Cognito.
- Cơ chế hoạt động của Access Token, ID Token và Refresh Token.
- Cách API Gateway xác thực JWT.
- Quy trình đăng nhập và phân quyền trong ứng dụng.

---

## Kết quả

Hoàn thành hệ thống xác thực người dùng và bảo vệ các API bằng JWT, tạo nền tảng bảo mật cho ứng dụng.