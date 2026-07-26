+++
title = "1.6 Tuần 6 - Xây dựng chức năng Text-to-Speech"
weight = 6

[params]
  collapsibleMenu = true
+++

## Mục tiêu

- Tìm hiểu dịch vụ Amazon Polly.
- Xây dựng chức năng chuyển văn bản thành giọng nói.
- Kết nối Amazon Polly với Backend Serverless.
- Hoàn thiện API phục vụ cho chức năng Text-to-Speech.

---

## Nội dung thực hiện

Trong tuần thứ sáu, tôi tập trung nghiên cứu dịch vụ Amazon Polly nhằm xây dựng chức năng chuyển đổi văn bản thành giọng nói (Text-to-Speech) cho ứng dụng.

Đầu tiên, tôi tìm hiểu các tính năng của Amazon Polly như các loại giọng đọc, ngôn ngữ hỗ trợ, các Engine tổng hợp giọng nói và định dạng âm thanh đầu ra.

Sau đó, tôi tiến hành tích hợp Amazon Polly vào các hàm AWS Lambda đã xây dựng ở các tuần trước. Lambda sẽ tiếp nhận nội dung văn bản từ người dùng, gửi yêu cầu đến Amazon Polly để tổng hợp giọng nói và trả kết quả về cho ứng dụng.

Các công việc đã thực hiện gồm:

- Tìm hiểu Amazon Polly và AWS SDK.
- Tích hợp Amazon Polly vào AWS Lambda.
- Xây dựng API chuyển văn bản thành giọng nói.
- Thiết lập các tham số như Voice, Engine và định dạng âm thanh.
- Kiểm thử chức năng Text-to-Speech với nhiều nội dung khác nhau.
- Xử lý các lỗi phát sinh trong quá trình tích hợp.

---

## Kiến thức đạt được

Sau tuần thứ sáu, tôi hiểu được:

- Nguyên lý hoạt động của Amazon Polly.
- Quy trình chuyển đổi văn bản thành giọng nói.
- Cách sử dụng AWS SDK để gọi các dịch vụ AWS.
- Cách tích hợp dịch vụ AI vào ứng dụng Serverless.
- Quy trình xử lý dữ liệu giữa Frontend, Backend và Amazon Polly.

---

## Kết quả

Hoàn thành chức năng Text-to-Speech của ứng dụng. Người dùng có thể nhập văn bản và nhận được kết quả là tệp âm thanh được tổng hợp bằng Amazon Polly thông qua hệ thống Backend Serverless.