+++
title = "1.5 Tuần 5 - Xây dựng hệ thống xác thực với Amazon Cognito"
weight = 5

[params]
  collapsibleMenu = true
+++

# Tuần 5 - Xây dựng hệ thống xác thực với Amazon Cognito

## Mục tiêu

Trong tuần thứ năm, tôi triển khai hệ thống xác thực người dùng cho ứng dụng bằng Amazon Cognito. Mục tiêu là xây dựng chức năng đăng ký và đăng nhập, tích hợp xác thực vào ứng dụng React, đồng thời bảo vệ các API thông qua cơ chế JWT Authorizer của Amazon API Gateway.

---

# 5.1 Tìm hiểu Amazon Cognito

Amazon Cognito là dịch vụ quản lý người dùng và xác thực của AWS, cho phép xây dựng hệ thống đăng ký, đăng nhập và quản lý phiên làm việc mà không cần tự xây dựng cơ sở dữ liệu người dùng.

Trong quá trình học, tôi tìm hiểu các thành phần chính của Amazon Cognito:

- User Pool
- App Client
- Authentication
- Authorization
- JSON Web Token (JWT)

Thông qua nội dung này, tôi hiểu được Cognito giúp đơn giản hóa việc quản lý người dùng và nâng cao tính bảo mật cho ứng dụng.

> **Chèn hình:** Tổng quan Amazon Cognito.

---

# 5.2 Tạo User Pool

Đầu tiên, tôi tiến hành tạo User Pool để lưu trữ thông tin người dùng.

Các bước thực hiện:

Amazon Cognito → User Pools → Create User Pool

Sau đó cấu hình:

- Authentication method
- Sign-in options
- Password policy
- MFA (không sử dụng trong dự án)
- User Pool Name

Sau khi hoàn thành, AWS tạo thành công User Pool.

Đây là nơi lưu trữ toàn bộ thông tin tài khoản của người dùng.

> **Chèn hình:** Tạo User Pool.

---

# 5.3 Tạo App Client

Sau khi tạo User Pool, tôi tạo App Client để ứng dụng React có thể giao tiếp với Amazon Cognito.

Các bước thực hiện:

User Pool → App Clients → Create App Client

Sau đó cấu hình:

- Application Type: SPA (Single-page Application)
- App Client Name
- Authentication Flow

Sau khi hoàn tất, AWS cung cấp:

- Client ID

Client ID sẽ được sử dụng trong quá trình tích hợp với ứng dụng React.

> **Chèn hình:** App Client.

---

# 5.4 Cấu hình Redirect URI

Tiếp theo, tôi cấu hình Redirect URI để xác định địa chỉ mà Cognito sẽ chuyển hướng sau khi người dùng hoàn thành quá trình xác thực.

Trong quá trình phát triển, tôi sử dụng địa chỉ của ứng dụng React chạy trên môi trường cục bộ (localhost).

Khi triển khai ứng dụng lên AWS Amplify, Redirect URI được cập nhật thành tên miền của ứng dụng.

Thông qua nội dung này, tôi hiểu được vai trò của Redirect URI trong quy trình xác thực người dùng.

> **Chèn hình:** Redirect URI.

---

# 5.5 Tích hợp Cognito với ứng dụng React

Sau khi hoàn tất cấu hình Cognito, tôi bắt đầu tích hợp chức năng xác thực vào Frontend.

Các nội dung thực hiện gồm:

- Kết nối ứng dụng React với User Pool.
- Cấu hình Client ID.
- Xây dựng chức năng đăng ký tài khoản.
- Xây dựng chức năng đăng nhập.
- Xây dựng chức năng đăng xuất.
- Kiểm tra trạng thái đăng nhập của người dùng.

Sau khi hoàn thành, người dùng có thể đăng ký và đăng nhập trực tiếp từ giao diện ứng dụng.

> **Chèn hình:** Giao diện đăng nhập.

---

# 5.6 Xây dựng chức năng đăng ký

Tôi triển khai chức năng đăng ký người dùng.

Quy trình hoạt động:

- Người dùng nhập Email và Mật khẩu.
- Ứng dụng gửi yêu cầu tới Amazon Cognito.
- Cognito tạo tài khoản mới.
- Người dùng nhập mã xác thực được gửi qua Email.
- Tài khoản được kích hoạt.

Thông qua quá trình này, tôi hiểu được quy trình xác thực tài khoản bằng Email Verification.

> **Chèn hình:** Đăng ký tài khoản.

---

# 5.7 Xây dựng chức năng đăng nhập

Sau khi tài khoản được kích hoạt, tôi triển khai chức năng đăng nhập.

Quy trình thực hiện:

- Người dùng nhập Email.
- Người dùng nhập Mật khẩu.
- React gửi yêu cầu tới Cognito.
- Cognito xác thực thông tin.
- Trả về các JWT Token.

Sau khi đăng nhập thành công, ứng dụng lưu thông tin phiên làm việc để người dùng có thể tiếp tục sử dụng các chức năng của hệ thống.

> **Chèn hình:** Đăng nhập thành công.

---

# 5.8 Tìm hiểu JWT Token

Sau khi đăng nhập thành công, Cognito trả về các Token.

Tôi tìm hiểu ba loại Token chính:

### ID Token

Chứa thông tin của người dùng như:

- User ID
- Email
- Username

---

### Access Token

Được sử dụng để xác thực khi gọi các API được bảo vệ.

Frontend sẽ gửi Access Token trong Header của HTTP Request.

---

### Refresh Token

Được sử dụng để cấp lại Access Token khi Access Token hết hạn mà người dùng không cần đăng nhập lại.

Thông qua nội dung này, tôi hiểu được quy trình quản lý phiên làm việc của ứng dụng.

> **Chèn hình:** JWT Token.

---

# 5.9 Cấu hình JWT Authorizer

Sau khi chức năng đăng nhập hoạt động, tôi tiến hành bảo vệ các API.

Các bước thực hiện:

API Gateway → Authorization → Create Authorizer

Sau đó cấu hình:

- Authorizer Type: JWT
- Issuer
- Audience (App Client ID)

Tiếp theo, tôi gán JWT Authorizer cho các Route cần bảo vệ.

Thông qua nội dung này, API Gateway sẽ tự động kiểm tra Access Token trước khi chuyển yêu cầu tới Lambda.

> **Chèn hình:** JWT Authorizer.

---

# 5.10 Kiểm thử hệ thống xác thực

Sau khi hoàn thiện toàn bộ hệ thống, tôi tiến hành kiểm thử.

Các nội dung kiểm thử gồm:

- Đăng ký tài khoản mới.
- Xác thực Email.
- Đăng nhập.
- Gọi API khi đã đăng nhập.
- Gọi API khi chưa đăng nhập.
- Kiểm tra Access Token không hợp lệ.
- Kiểm tra Access Token hết hạn.

Kết quả cho thấy các API được bảo vệ đúng theo yêu cầu và chỉ người dùng đã xác thực mới có thể truy cập.

> **Chèn hình:** Kiểm thử JWT.

---

# 5.11 Khó khăn gặp phải

Trong quá trình triển khai, tôi gặp một số khó khăn khi cấu hình User Pool, App Client và Redirect URI do các tham số này cần thống nhất với ứng dụng React.

Bên cạnh đó, việc tích hợp JWT Authorizer vào Amazon API Gateway cũng đòi hỏi cấu hình chính xác Issuer và Audience để API Gateway có thể xác thực Access Token.

---

# 5.12 Cách giải quyết

Để khắc phục các vấn đề trên, tôi kiểm tra lại cấu hình của User Pool, App Client và API Gateway, đồng thời đối chiếu với tài liệu chính thức của AWS.

Ngoài ra, tôi thực hiện kiểm thử nhiều lần với các trường hợp đăng nhập thành công, đăng nhập thất bại và Access Token không hợp lệ để đảm bảo hệ thống xác thực hoạt động ổn định.

---

# 5.13 Kiến thức đạt được

Sau tuần thứ năm, tôi đã:

- Hiểu cơ chế xác thực của Amazon Cognito.
- Thành thạo quy trình tạo User Pool và App Client.
- Biết cách tích hợp Cognito với ứng dụng React.
- Xây dựng chức năng đăng ký và đăng nhập người dùng.
- Hiểu cơ chế hoạt động của ID Token, Access Token và Refresh Token.
- Biết cách cấu hình JWT Authorizer trong Amazon API Gateway.
- Bảo vệ thành công các API bằng cơ chế xác thực JWT.

---

# 5.14 Đánh giá của bản thân

Tuần thứ năm giúp tôi hiểu rõ quy trình xây dựng một hệ thống xác thực người dùng trên nền tảng AWS. Việc kết hợp Amazon Cognito với React và Amazon API Gateway giúp tôi nắm được cách triển khai cơ chế xác thực hiện đại mà không cần tự phát triển hệ thống quản lý tài khoản từ đầu.

Sau khi hoàn thành tuần này, hệ thống đã có khả năng quản lý người dùng và bảo vệ các API thông qua JWT, tạo nền tảng bảo mật để tiếp tục phát triển chức năng chuyển văn bản thành giọng nói bằng Amazon Polly trong tuần tiếp theo.