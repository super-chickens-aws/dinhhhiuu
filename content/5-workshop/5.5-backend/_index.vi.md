+++
title = '5.5 Triển khai Backend'
weight = 5

[params]
  collapsibleMenu = true
+++

## Giới thiệu

Trong phần này, chúng ta sẽ triển khai toàn bộ **Backend** cho ứng dụng **Polly Voice** bằng các dịch vụ Serverless của AWS.

Backend có nhiệm vụ tiếp nhận yêu cầu từ frontend, xử lý việc chuyển đổi văn bản thành giọng nói bằng Amazon Polly, lưu trữ tệp âm thanh trên Amazon S3, ghi nhận lịch sử vào Amazon DynamoDB và trả kết quả về cho người dùng thông qua Amazon API Gateway.

Toàn bộ hệ thống được xây dựng trên các dịch vụ managed của AWS, giúp giảm chi phí vận hành, tự động mở rộng và không cần quản lý máy chủ.

---

## Nội dung thực hiện

Trong phần này, chúng ta sẽ lần lượt thực hiện các bước sau:

1. **Tạo bảng Amazon DynamoDB** để lưu lịch sử chuyển đổi.
2. **Tạo Amazon S3 Bucket** để lưu trữ các tệp âm thanh MP3.
3. **Tạo và cấu hình AWS Lambda Function**, đồng thời kết nối với Amazon Polly, Amazon S3 và Amazon DynamoDB để xử lý toàn bộ nghiệp vụ của ứng dụng.
4. **Cấu hình Amazon API Gateway** để cung cấp REST API cho frontend và chuyển tiếp các yêu cầu đến Lambda.
5. **Kiểm tra Backend** nhằm đảm bảo toàn bộ hệ thống hoạt động chính xác trước khi triển khai frontend.

---

## Kết quả mong đợi

Sau khi hoàn thành phần này, chúng ta sẽ có một hệ thống Backend hoàn chỉnh với các thành phần sau:

- Amazon DynamoDB lưu lịch sử chuyển đổi.
- Amazon S3 lưu trữ tệp âm thanh.
- AWS Lambda xử lý nghiệp vụ.
- Amazon API Gateway cung cấp API.
- Amazon Polly tạo giọng nói từ văn bản.

Backend sau khi hoàn tất sẽ sẵn sàng để kết nối với frontend trong phần tiếp theo.