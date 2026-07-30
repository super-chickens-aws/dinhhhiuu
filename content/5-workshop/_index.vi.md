+++
title = "5. Workshop"
weight = 5

[params]
  collapsibleMenu = true
+++

## Tổng quan

**Xây dựng ứng dụng Polly Voice trên kiến trúc AWS Serverless**

**Polly Voice** là một ứng dụng web chuyển đổi văn bản thành giọng nói (Text-to-Speech - TTS) được xây dựng hoàn toàn trên nền tảng **Amazon Web Services (AWS)** theo kiến trúc **Serverless**.

Ứng dụng cho phép người dùng đăng ký tài khoản, đăng nhập, nhập nội dung văn bản, lựa chọn giọng đọc và tạo tệp âm thanh MP3 bằng dịch vụ **Amazon Polly**. Sau khi quá trình tổng hợp giọng nói hoàn tất, các tệp âm thanh được lưu trữ trên **Amazon S3**, trong khi lịch sử chuyển đổi được lưu trong **Amazon DynamoDB**, cho phép người dùng xem lại hoặc tải xuống các bản ghi đã tạo bất cứ lúc nào.

Trong workshop này, toàn bộ hệ thống sẽ được triển khai bằng các dịch vụ được quản lý hoàn toàn của AWS (Fully Managed Services), giúp loại bỏ việc quản lý máy chủ, giảm chi phí vận hành và dễ dàng mở rộng khi số lượng người dùng tăng lên.

Thông qua workshop, chúng ta sẽ hiểu cách nhiều dịch vụ AWS phối hợp với nhau để xây dựng một ứng dụng web hoàn chỉnh theo mô hình cloud-native, bao gồm xác thực người dùng, xử lý nghiệp vụ ở backend, lưu trữ dữ liệu và triển khai giao diện người dùng.

---

## Nội dung Workshop

Workshop được chia thành các phần sau:

1. [Tổng quan](5.1-Overview/)
2. [Chuẩn bị](5.2-Prerequisites/)
3. [Kiến trúc giải pháp](5.3-Architecture/)
4. [Triển khai Backend](5.4-Backend/)
5. [Triển khai Frontend](5.5-Frontend/)
6. [Kiểm thử toàn bộ hệ thống](5.6-Testing/)
7. [Giám sát và bảo mật](5.7-Monitoring/)
8. [Dọn dẹp tài nguyên](5.8-Cleanup/)

Sau khi hoàn thành workshop, chúng ta sẽ triển khai thành công một ứng dụng **Text-to-Speech** hoàn chỉnh, tuân theo kiến trúc **AWS Serverless** hiện đại và các nguyên tắc bảo mật theo AWS Best Practices.