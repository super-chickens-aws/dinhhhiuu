+++
title = "1.5 Tuần 5 - Xây dựng hệ thống xác thực với Amazon Cognito"
weight = 5

[params]
  collapsibleMenu = true
+++

## Mục tiêu

Trong tuần thứ năm, tôi triển khai hệ thống xác thực người dùng cho ứng dụng bằng Amazon Cognito. Mục tiêu là xây dựng chức năng đăng ký và đăng nhập, tích hợp xác thực vào ứng dụng React, đồng thời bảo vệ các API thông qua cơ chế JWT Authorizer của Amazon API Gateway.

---

## 5.1 Tìm hiểu Amazon Cognito

**Amazon Cognito** là dịch vụ quản lý danh tính và xác thực người dùng của AWS, cho phép xây dựng hệ thống đăng ký, đăng nhập và quản lý phiên làm việc mà không cần tự phát triển cơ sở dữ liệu người dùng.

Đối với các ứng dụng Web và Mobile, Amazon Cognito cung cấp sẵn các cơ chế xác thực, phân quyền và quản lý thông tin người dùng, giúp giảm thời gian phát triển và nâng cao tính bảo mật của hệ thống.

Trong quá trình học, tôi tìm hiểu các thành phần chính của Amazon Cognito như sau:

| Thành phần | Mô tả |
|------------|------|
| **User Pool** | Là nơi lưu trữ thông tin người dùng, quản lý tài khoản, mật khẩu và các phương thức xác thực. Đây là thành phần chịu trách nhiệm xử lý quá trình đăng ký, đăng nhập và quản lý người dùng. |
| **App Client** | Đại diện cho ứng dụng sẽ sử dụng User Pool để xác thực người dùng. Mỗi ứng dụng (Web, Mobile...) sẽ được cấp một **Client ID** để kết nối với Cognito. |
| **Authentication** | Quá trình xác minh danh tính của người dùng thông qua thông tin đăng nhập như Email, Username và Password trước khi cho phép truy cập hệ thống. |
| **Authorization** | Quá trình xác định quyền truy cập của người dùng sau khi đăng nhập thành công. Trong dự án, API Gateway sử dụng JWT để kiểm tra người dùng có được phép sử dụng API hay không. |
| **JSON Web Token (JWT)** | Chuỗi mã hóa chứa thông tin xác thực của người dùng sau khi đăng nhập thành công. JWT được gửi kèm trong mỗi yêu cầu đến Backend để chứng minh người dùng đã được xác thực. |

Thông qua việc tìm hiểu các thành phần trên, tôi hiểu được quy trình xác thực của Amazon Cognito gồm các bước cơ bản:

1. Người dùng đăng ký hoặc đăng nhập thông qua ứng dụng.
2. Amazon Cognito kiểm tra thông tin xác thực.
3. Nếu đăng nhập thành công, Cognito tạo và trả về các **JWT Token**.
4. Ứng dụng lưu trữ Token và gửi kèm trong các yêu cầu đến Backend.
5. Amazon API Gateway sử dụng JWT Authorizer để xác thực Token trước khi chuyển yêu cầu đến AWS Lambda.

Qua nội dung này, tôi hiểu được Amazon Cognito giúp đơn giản hóa việc quản lý người dùng, giảm khối lượng công việc khi xây dựng hệ thống xác thực và tăng cường tính bảo mật cho ứng dụng nhờ sử dụng cơ chế xác thực dựa trên JSON Web Token (JWT).

---

## 5.2 Tạo User Pool

Sau khi tìm hiểu về Amazon Cognito, tôi tiến hành tạo **User Pool** để quản lý thông tin và xác thực người dùng cho ứng dụng.

Các bước thực hiện: **Amazon Cognito → User Pools → Create User Pool**

Sau đó cấu hình các thông tin cơ bản:

- Authentication application: **Single-page application (SPA)**
- App client name
- Sign-in options
- Allowed callback URL
- Allowed sign-out URL

Sau khi hoàn tất cấu hình, tôi nhấn **Create User Pool** để khởi tạo.

User Pool sẽ lưu trữ thông tin tài khoản người dùng và cung cấp các chức năng như đăng ký, đăng nhập, xác thực và quản lý phiên làm việc cho ứng dụng.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog46.png)

---

# 5.3 Tạo App Client

Sau khi tạo User Pool, tôi tạo App Client để ứng dụng React có thể giao tiếp với Amazon Cognito.

Các bước thực hiện: **User Pool → App Clients → Create App Client**

Sau đó cấu hình:

- Application Type: SPA (Single-page Application)
- App Client Name
- Authentication Flow

Sau khi hoàn tất, AWS cung cấp: **Client ID**

Client ID sẽ được sử dụng trong quá trình tích hợp với ứng dụng React.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog47.png)

---

## 5.4 Cấu hình Redirect URI

Tiếp theo, tôi cấu hình Redirect URI để xác định địa chỉ mà Cognito sẽ chuyển hướng sau khi người dùng hoàn thành quá trình xác thực.

Trong quá trình phát triển, tôi sử dụng địa chỉ của ứng dụng React chạy trên môi trường cục bộ (localhost).

Khi triển khai ứng dụng lên AWS Amplify, Redirect URI được cập nhật thành tên miền của ứng dụng.

Thông qua nội dung này, tôi hiểu được vai trò của Redirect URI trong quy trình xác thực người dùng.

---

## 5.5 Tích hợp Cognito với ứng dụng React

Sau khi hoàn tất cấu hình Amazon Cognito, tôi tiến hành tích hợp chức năng xác thực người dùng vào ứng dụng React.

Đầu tiên, tôi cấu hình các thông tin của User Pool và App Client trong ứng dụng để React có thể giao tiếp với Amazon Cognito.

Các nội dung thực hiện gồm:

- Kết nối ứng dụng React với Amazon Cognito.
- Cấu hình User Pool ID và App Client ID.
- Xây dựng chức năng đăng ký tài khoản.
- Xây dựng chức năng đăng nhập.
- Xây dựng chức năng đăng xuất.
- Kiểm tra trạng thái đăng nhập của người dùng.

Ví dụ cấu hình kết nối:

```javascript
export const authConfig = {
    userPoolId: "ap-southeast-1_xxxxxxxx",
    clientId: "3l8g0j7vxxxxxxxxxxxx"
};
```

Sau khi hoàn thành cấu hình, ứng dụng React có thể sử dụng các thông tin này để thực hiện đăng ký và đăng nhập thông qua Amazon Cognito.

---

## 5.6 Xây dựng chức năng đăng ký

Tiếp theo, tôi xây dựng chức năng đăng ký tài khoản cho người dùng.

Quy trình hoạt động:

1. Người dùng nhập Email và Mật khẩu.
2. React gửi yêu cầu đăng ký đến Amazon Cognito.
3. Cognito tạo tài khoản mới.
4. Cognito gửi mã xác thực (Verification Code) đến Email.
5. Người dùng nhập mã xác thực để kích hoạt tài khoản.

Ví dụ lời gọi hàm đăng ký:

```javascript
await register(email, password);
```

Sau khi đăng ký thành công, ứng dụng sẽ chuyển người dùng sang màn hình nhập mã xác thực để hoàn tất quá trình tạo tài khoản.

Thông qua nội dung này, tôi hiểu được quy trình xác thực tài khoản bằng Email Verification của Amazon Cognito.

---

## 5.7 Xây dựng chức năng đăng nhập

Sau khi tài khoản được kích hoạt, tôi tiếp tục xây dựng chức năng đăng nhập.

Quy trình hoạt động:

1. Người dùng nhập Email.
2. Người dùng nhập Mật khẩu.
3. React gửi yêu cầu đăng nhập đến Amazon Cognito.
4. Cognito xác thực thông tin người dùng.
5. Nếu hợp lệ, Cognito trả về các JWT Token.

Ví dụ lời gọi hàm đăng nhập:

```javascript
await login(email, password);
```

Sau khi đăng nhập thành công, ứng dụng sẽ nhận được các Token do Amazon Cognito cấp và lưu lại phiên đăng nhập của người dùng.

Các Token này sẽ được sử dụng khi gọi các API được bảo vệ thông qua Amazon API Gateway.

Thông qua quá trình này, tôi hiểu được quy trình xác thực người dùng và cách Amazon Cognito sử dụng JWT để bảo vệ hệ thống.

---

## 5.8 Tìm hiểu JWT Token

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

---

## 5.9 Cấu hình JWT Authorizer

Sau khi chức năng đăng nhập hoạt động, tôi tiến hành bảo vệ các API.

Các bước thực hiện: **API Gateway → Authorization → Create Authorizer**

Sau đó cấu hình:

- Authorizer Type: JWT
- Issuer
- Audience (App Client ID)

Tiếp theo, tôi gán JWT Authorizer cho các Route cần bảo vệ.

Thông qua nội dung này, API Gateway sẽ tự động kiểm tra Access Token trước khi chuyển yêu cầu tới Lambda.

---

## 5.10 Kiểm thử hệ thống xác thực

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

---

## 5.11 Khó khăn gặp phải

Trong quá trình triển khai, tôi gặp một số khó khăn khi cấu hình User Pool, App Client và Redirect URI do các tham số này cần thống nhất với ứng dụng React.

Bên cạnh đó, việc tích hợp JWT Authorizer vào Amazon API Gateway cũng đòi hỏi cấu hình chính xác Issuer và Audience để API Gateway có thể xác thực Access Token.

---

## 5.12 Cách giải quyết

Để khắc phục các vấn đề trên, tôi kiểm tra lại cấu hình của User Pool, App Client và API Gateway, đồng thời đối chiếu với tài liệu chính thức của AWS.

Ngoài ra, tôi thực hiện kiểm thử nhiều lần với các trường hợp đăng nhập thành công, đăng nhập thất bại và Access Token không hợp lệ để đảm bảo hệ thống xác thực hoạt động ổn định.

---

## 5.13 Kiến thức đạt được

Sau tuần thứ năm, tôi đã:

- Hiểu cơ chế xác thực của Amazon Cognito.
- Thành thạo quy trình tạo User Pool và App Client.
- Biết cách tích hợp Cognito với ứng dụng React.
- Xây dựng chức năng đăng ký và đăng nhập người dùng.
- Hiểu cơ chế hoạt động của ID Token, Access Token và Refresh Token.
- Biết cách cấu hình JWT Authorizer trong Amazon API Gateway.
- Bảo vệ thành công các API bằng cơ chế xác thực JWT.

---

## 5.14 Đánh giá của bản thân

Tuần thứ năm giúp tôi hiểu rõ quy trình xây dựng một hệ thống xác thực người dùng trên nền tảng AWS. Việc kết hợp Amazon Cognito với React và Amazon API Gateway giúp tôi nắm được cách triển khai cơ chế xác thực hiện đại mà không cần tự phát triển hệ thống quản lý tài khoản từ đầu.

Sau khi hoàn thành tuần này, hệ thống đã có khả năng quản lý người dùng và bảo vệ các API thông qua JWT, tạo nền tảng bảo mật để tiếp tục phát triển chức năng chuyển văn bản thành giọng nói bằng Amazon Polly trong tuần tiếp theo.