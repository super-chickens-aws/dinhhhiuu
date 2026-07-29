+++
title = "1.8 Tuần 8 - Hoàn thiện dự án và tổng kết"
weight = 8

[params]
  collapsibleMenu = true
+++

## Mục tiêu

Trong tuần cuối cùng của kỳ thực tập, tôi tập trung hoàn thiện sản phẩm, kiểm thử toàn bộ hệ thống, tối ưu mã nguồn và tài liệu kỹ thuật, đồng thời chuẩn bị báo cáo và sản phẩm demo cho đánh giá kết quả thực tập.

---

## 8.1 Rà soát toàn bộ hệ thống

Sau khi các chức năng chính đã hoàn thành, tôi tiến hành rà soát lại toàn bộ dự án nhằm đảm bảo hệ thống hoạt động ổn định trước khi bàn giao.

Các nội dung kiểm tra gồm:

- Cấu trúc mã nguồn.
- Cấu hình các dịch vụ AWS.
- Các API của hệ thống.
- Chức năng xác thực người dùng.
- Chức năng Text-to-Speech.
- Giao diện người dùng.

Thông qua quá trình này, tôi phát hiện và xử lý một số lỗi nhỏ còn tồn tại trong quá trình phát triển.

---

## 8.2 Kiểm thử chức năng

Tiếp theo, tôi thực hiện kiểm thử toàn bộ các chức năng của ứng dụng.

Các nội dung kiểm thử bao gồm:

### Chức năng người dùng

- Đăng ký tài khoản.
- Xác thực Email.
- Đăng nhập.
- Đăng xuất.

### Chức năng Text-to-Speech

- Nhập văn bản.
- Lựa chọn giọng đọc.
- Lựa chọn Engine.
- Tổng hợp giọng nói.
- Phát âm thanh.
- Tải xuống tệp âm thanh.

### Chức năng API

- Kiểm tra JWT Authorizer.
- Kiểm tra phản hồi của API.
- Kiểm tra các trường hợp dữ liệu không hợp lệ.

Kết quả cho thấy các chức năng đều hoạt động đúng theo thiết kế.

---

## 8.3 Tối ưu hệ thống

Sau khi kiểm thử, tôi tiến hành tối ưu hệ thống.

Các công việc thực hiện gồm:

- Chuẩn hóa cấu trúc thư mục của dự án.
- Tách riêng các lớp xử lý nghiệp vụ.
- Loại bỏ các đoạn mã không còn sử dụng.
- Chuẩn hóa định dạng phản hồi của API.
- Bổ sung xử lý ngoại lệ.
- Hoàn thiện ghi log phục vụ quá trình kiểm tra và bảo trì.

Việc tối ưu giúp mã nguồn rõ ràng hơn và thuận tiện cho việc mở rộng trong tương lai.

---

## 8.4 Hoàn thiện giao diện người dùng

Tiếp theo, tôi chỉnh sửa và hoàn thiện giao diện của ứng dụng.

Các nội dung thực hiện:

- Cải thiện bố cục giao diện.
- Đồng nhất màu sắc và thành phần hiển thị.
- Hoàn thiện thanh điều hướng.
- Bổ sung thông báo lỗi và thông báo thành công.
- Cải thiện trải nghiệm người dùng khi sử dụng chức năng Text-to-Speech.

Sau khi hoàn thiện, giao diện trở nên trực quan và dễ sử dụng hơn.

---

## 8.5 Hoàn thiện tài liệu kỹ thuật

Song song với việc hoàn thiện sản phẩm, tôi xây dựng và cập nhật tài liệu kỹ thuật.

Các tài liệu được bổ sung gồm:

- Hướng dẫn cài đặt dự án.
- Hướng dẫn triển khai trên AWS.
- Hướng dẫn cấu hình Amazon Cognito.
- Hướng dẫn cấu hình AWS Lambda.
- Hướng dẫn cấu hình Amazon API Gateway.
- Hướng dẫn triển khai Frontend bằng AWS Amplify.
- Hướng dẫn sử dụng ứng dụng.

Việc xây dựng tài liệu giúp người khác có thể dễ dàng triển khai và sử dụng hệ thống.

---

## 8.6 Hoàn thiện sơ đồ kiến trúc hệ thống

Để phục vụ báo cáo và quá trình bàn giao, tôi tổng hợp và hoàn thiện sơ đồ kiến trúc của hệ thống.

Kiến trúc bao gồm các thành phần:

- React Frontend.
- AWS Amplify.
- Amazon Cognito.
- Amazon API Gateway.
- AWS Lambda.
- Amazon Polly.

Sơ đồ thể hiện luồng xử lý từ người dùng đến các dịch vụ AWS và ngược lại.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog53.png)

---

## 8.7 Chuẩn bị báo cáo và sản phẩm demo

Sau khi sản phẩm hoàn thiện, tôi tiến hành chuẩn bị cho buổi đánh giá cuối kỳ.

Các công việc thực hiện gồm:

- Tổng hợp quá trình thực tập.
- Hoàn thiện báo cáo.
- Chuẩn bị hình ảnh minh họa.
- Chuẩn bị tài liệu trình bày.
- Kiểm tra lại toàn bộ ứng dụng trước khi demo.

Qua quá trình này, tôi có cái nhìn tổng quan hơn về toàn bộ dự án và quá trình phát triển.

---

## 8.8 Khó khăn gặp phải

Trong giai đoạn hoàn thiện, tôi gặp một số khó khăn khi rà soát lại toàn bộ hệ thống do ứng dụng đã tích hợp nhiều dịch vụ AWS khác nhau.

Ngoài ra, việc đảm bảo các chức năng hoạt động ổn định sau khi triển khai và cập nhật tài liệu đầy đủ cũng đòi hỏi nhiều thời gian và sự cẩn thận.

---

## 8.9 Cách giải quyết

Để khắc phục các vấn đề trên, tôi xây dựng danh sách các chức năng cần kiểm thử và thực hiện kiểm tra theo từng nhóm chức năng.

Bên cạnh đó, tôi rà soát lại toàn bộ cấu hình của các dịch vụ AWS, cập nhật tài liệu song song với quá trình hoàn thiện mã nguồn và kiểm thử lại sau mỗi lần chỉnh sửa nhằm đảm bảo hệ thống luôn hoạt động ổn định.

---

## 8.10 Kiến thức đạt được

Sau tuần thứ tám, tôi đã:

- Hiểu quy trình hoàn thiện và bàn giao một dự án phần mềm.
- Thành thạo việc kiểm thử và đánh giá chất lượng hệ thống.
- Biết cách tối ưu mã nguồn và cấu trúc dự án.
- Hoàn thiện tài liệu kỹ thuật phục vụ triển khai và bảo trì.
- Hiểu quy trình triển khai và vận hành một ứng dụng Cloud trên AWS.
- Có kinh nghiệm tích hợp nhiều dịch vụ AWS trong cùng một hệ thống.

---

## 8.11 Kết quả đạt được

Sau tám tuần thực tập, tôi đã hoàn thành ứng dụng Web chuyển văn bản thành giọng nói (Text-to-Speech) được xây dựng theo kiến trúc Serverless trên nền tảng Amazon Web Services.

Hệ thống bao gồm các thành phần chính:

- Frontend được phát triển bằng React và triển khai trên AWS Amplify.
- Hệ thống xác thực người dùng sử dụng Amazon Cognito.
- Backend được xây dựng bằng AWS Lambda.
- Các API được quản lý thông qua Amazon API Gateway.
- Chức năng chuyển văn bản thành giọng nói được triển khai bằng Amazon Polly.

Ứng dụng cho phép người dùng đăng ký tài khoản, đăng nhập, nhập nội dung văn bản, lựa chọn giọng đọc và nhận kết quả là tệp âm thanh được tổng hợp tự động.

---

## 8.12 Đánh giá của bản thân

Kỳ thực tập kéo dài tám tuần đã giúp tôi có cơ hội tiếp cận quy trình phát triển một ứng dụng Cloud trên nền tảng Amazon Web Services từ giai đoạn tìm hiểu kiến thức nền tảng đến thiết kế, triển khai, kiểm thử và hoàn thiện sản phẩm.

Thông qua dự án, tôi không chỉ hiểu rõ hơn về các dịch vụ như Amazon Cognito, AWS Lambda, Amazon API Gateway, Amazon Polly và AWS Amplify mà còn rèn luyện được kỹ năng thiết kế hệ thống, lập trình, kiểm thử và giải quyết các vấn đề phát sinh trong quá trình phát triển.

Đây là nền tảng quan trọng để tôi tiếp tục nghiên cứu các kiến trúc Cloud hiện đại và áp dụng những kiến thức đã học vào các dự án thực tế trong tương lai.