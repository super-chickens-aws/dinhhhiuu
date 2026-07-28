+++
title = "1.7 Tuần 7 - Tích hợp hệ thống và triển khai ứng dụng"
weight = 7

[params]
  collapsibleMenu = true
+++

# Tuần 7 - Tích hợp hệ thống và triển khai ứng dụng

## Mục tiêu

Trong tuần thứ bảy, tôi hoàn thiện giao diện người dùng, tích hợp toàn bộ các thành phần của hệ thống và triển khai ứng dụng lên môi trường Cloud. Mục tiêu là đảm bảo Frontend, Backend và các dịch vụ AWS hoạt động đồng bộ, đồng thời đưa ứng dụng vào trạng thái sẵn sàng sử dụng.

---

# 7.1 Hoàn thiện giao diện người dùng

Sau khi các chức năng Backend đã hoàn thành, tôi tiếp tục phát triển giao diện người dùng bằng React.

Các giao diện được xây dựng gồm:

- Trang đăng ký.
- Trang đăng nhập.
- Trang Text-to-Speech.
- Thanh điều hướng (Navigation Bar).
- Khu vực hiển thị kết quả.

Bên cạnh đó, tôi cải thiện bố cục giao diện nhằm giúp người dùng thao tác dễ dàng hơn.

> **Chèn hình:** Giao diện tổng quan của ứng dụng.

---

# 7.2 Hoàn thiện chức năng Text-to-Speech

Tiếp theo, tôi hoàn thiện giao diện cho chức năng chuyển văn bản thành giọng nói.

Các chức năng được bổ sung gồm:

- Nhập văn bản.
- Lựa chọn giọng đọc.
- Lựa chọn Engine.
- Thiết lập định dạng âm thanh.
- Phát âm thanh sau khi tổng hợp.
- Tải xuống tệp âm thanh.

Ngoài ra, tôi bổ sung các thông báo lỗi và trạng thái xử lý nhằm cải thiện trải nghiệm người dùng.

> **Chèn hình:** Giao diện Text-to-Speech.

---

# 7.3 Kết nối Frontend với Backend

Sau khi giao diện hoàn thành, tôi tiến hành kết nối React với Backend Serverless.

Các công việc thực hiện gồm:

- Gửi HTTP Request tới Amazon API Gateway.
- Nhận Response từ AWS Lambda.
- Hiển thị kết quả trên giao diện.
- Xử lý lỗi khi API trả về kết quả không hợp lệ.

Sau khi hoàn tất, toàn bộ chức năng Text-to-Speech có thể hoạt động trực tiếp từ giao diện Web.

> **Chèn hình:** Frontend gọi API Gateway.

---

# 7.4 Tích hợp Amazon Cognito

Tiếp theo, tôi tích hợp hệ thống xác thực người dùng vào giao diện.

Các chức năng được triển khai:

- Đăng ký tài khoản.
- Xác thực Email.
- Đăng nhập.
- Đăng xuất.
- Kiểm tra trạng thái đăng nhập.

Sau khi người dùng đăng nhập thành công, Access Token được sử dụng để gọi các API yêu cầu xác thực.

> **Chèn hình:** Đăng nhập thành công.

---

# 7.5 Gọi API có xác thực

Sau khi Cognito hoạt động ổn định, tôi bổ sung Access Token vào Header của các HTTP Request.

Ví dụ:

```text
Authorization: Bearer <Access Token>
```

Amazon API Gateway sử dụng JWT Authorizer để kiểm tra Access Token trước khi chuyển yêu cầu tới AWS Lambda.

Qua nội dung này, tôi hoàn thiện cơ chế bảo vệ API của hệ thống.

> **Chèn hình:** JWT Authorizer hoạt động.

---

# 7.6 Triển khai ứng dụng bằng AWS Amplify

Sau khi hoàn thiện toàn bộ chức năng, tôi tiến hành triển khai Frontend lên AWS Amplify.

Các bước thực hiện:

- Kết nối AWS Amplify với GitHub.
- Chọn Repository của dự án.
- Chọn nhánh triển khai.
- Thiết lập Build Command.
- Thiết lập thư mục Build Output.
- Thực hiện Deploy.

Sau khi quá trình triển khai hoàn tất, AWS Amplify tự động cung cấp một địa chỉ để truy cập ứng dụng thông qua Internet.

> **Chèn hình:** AWS Amplify Deploy.

---

# 7.7 Cấu hình Environment Variables

Để Frontend có thể kết nối với Backend, tôi cấu hình các biến môi trường trên AWS Amplify.

Các biến được sử dụng gồm:

- URL của Amazon API Gateway.
- User Pool ID.
- App Client ID.
- AWS Region.

Việc quản lý thông tin thông qua Environment Variables giúp dễ dàng thay đổi cấu hình giữa các môi trường phát triển và triển khai mà không cần chỉnh sửa trực tiếp mã nguồn.

> **Chèn hình:** Environment Variables.

---

# 7.8 Kiểm thử toàn bộ hệ thống

Sau khi triển khai thành công, tôi tiến hành kiểm thử toàn bộ ứng dụng.

Các nội dung kiểm thử gồm:

- Đăng ký tài khoản.
- Xác thực Email.
- Đăng nhập.
- Đăng xuất.
- Chuyển văn bản thành giọng nói.
- Phát âm thanh.
- Tải xuống tệp âm thanh.
- Kiểm tra các API yêu cầu xác thực.

Kết quả cho thấy các chức năng chính đều hoạt động đúng theo thiết kế.

> **Chèn hình:** Kết quả kiểm thử.

---

# 7.9 Tự động triển khai từ GitHub

Ngoài việc triển khai lần đầu, tôi tìm hiểu cơ chế Continuous Deployment của AWS Amplify.

Mỗi khi mã nguồn được cập nhật lên nhánh GitHub đã cấu hình:

- AWS Amplify tự động tải mã nguồn.
- Thực hiện Build.
- Triển khai phiên bản mới.

Nhờ đó, quá trình cập nhật ứng dụng trở nên nhanh chóng và giảm thao tác thủ công.

> **Chèn hình:** Quy trình CI/CD của AWS Amplify.

---

# 7.10 Khó khăn gặp phải

Trong quá trình tích hợp và triển khai, tôi gặp một số khó khăn khi kết nối Frontend với Backend do cấu hình URL của API Gateway và các biến môi trường cần được thiết lập chính xác.

Ngoài ra, việc đồng bộ cấu hình giữa Amazon Cognito, API Gateway và AWS Amplify cũng đòi hỏi kiểm tra cẩn thận để đảm bảo quá trình xác thực hoạt động ổn định sau khi triển khai.

---

# 7.11 Cách giải quyết

Để khắc phục các vấn đề trên, tôi kiểm tra lại cấu hình Environment Variables, xác nhận địa chỉ Endpoint của API Gateway và thực hiện triển khai lại ứng dụng sau mỗi lần thay đổi.

Bên cạnh đó, tôi kiểm thử toàn bộ quy trình từ đăng nhập đến sử dụng chức năng Text-to-Speech nhằm phát hiện và xử lý kịp thời các lỗi phát sinh.

---

# 7.12 Kiến thức đạt được

Sau tuần thứ bảy, tôi đã:

- Hoàn thiện giao diện người dùng bằng React.
- Tích hợp Frontend với Backend Serverless.
- Sử dụng Access Token để gọi các API được bảo vệ.
- Hiểu quy trình triển khai ứng dụng bằng AWS Amplify.
- Biết cách quản lý Environment Variables.
- Hiểu cơ chế Continuous Deployment từ GitHub.
- Hoàn thiện việc tích hợp toàn bộ hệ thống.

---

# 7.13 Đánh giá của bản thân

Tuần thứ bảy là giai đoạn hoàn thiện và tích hợp toàn bộ hệ thống. Việc kết nối thành công Frontend với Backend, đồng thời triển khai ứng dụng lên AWS Amplify giúp tôi hiểu rõ hơn quy trình đưa một ứng dụng Web từ môi trường phát triển lên môi trường thực tế.

Thông qua quá trình này, tôi có cơ hội làm quen với quy trình triển khai, quản lý cấu hình và kiểm thử hệ thống sau khi phát hành. Đây là những kỹ năng quan trọng trong quá trình phát triển và vận hành các ứng dụng Cloud trên nền tảng AWS.