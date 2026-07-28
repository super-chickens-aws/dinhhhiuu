+++
title = "1.3 Tuần 3 - Tìm hiểu Amazon VPC và Networking"
weight = 3

[params]
  collapsibleMenu = true
+++

# Tuần 3 - Tìm hiểu Amazon VPC và Networking

## Mục tiêu

Trong tuần thứ ba, tôi tập trung nghiên cứu kiến trúc mạng trên nền tảng AWS. Mục tiêu là hiểu cách xây dựng một hệ thống mạng riêng (Virtual Private Cloud), cách các thành phần mạng giao tiếp với nhau và cách thiết kế hạ tầng mạng đảm bảo tính bảo mật, khả năng mở rộng và tính sẵn sàng cho ứng dụng.

---

# 3.1 Tìm hiểu Amazon VPC

Amazon Virtual Private Cloud (Amazon VPC) là dịch vụ cho phép người dùng xây dựng một mạng riêng trên nền tảng AWS để triển khai các tài nguyên như EC2, RDS hay Lambda.

Khác với việc triển khai trực tiếp trên Internet, VPC giúp cô lập tài nguyên, kiểm soát lưu lượng mạng và tăng cường bảo mật cho hệ thống.

Trong nội dung này, tôi tìm hiểu:

- Khái niệm Virtual Private Cloud.
- Thành phần của VPC.
- Cách AWS tổ chức hệ thống mạng.
- Mối quan hệ giữa VPC và các dịch vụ AWS.

> **Chèn hình:** Tổng quan Amazon VPC.

---

# 3.2 Tạo Virtual Private Cloud

Sau khi tìm hiểu lý thuyết, tôi tiến hành tạo một VPC mới.

Các bước thực hiện:

VPC → Create VPC

Sau đó cấu hình:

- Name
- IPv4 CIDR Block
- IPv6 (không sử dụng)
- Tenancy

Ví dụ:

- CIDR Block: **10.0.0.0/16**

Sau khi hoàn thành, AWS tạo thành công một VPC mới.

Qua nội dung này, tôi hiểu rằng CIDR Block quyết định phạm vi địa chỉ IP có thể sử dụng trong toàn bộ hệ thống mạng.

> **Chèn hình:** Tạo VPC.

---

# 3.3 Tìm hiểu Subnet

Sau khi tạo VPC, tôi tiếp tục tìm hiểu Subnet.

Subnet là một phần mạng nhỏ nằm bên trong VPC.

AWS cho phép tạo nhiều Subnet để phân chia hệ thống thành nhiều vùng mạng khác nhau.

Tôi nghiên cứu hai loại Subnet:

- Public Subnet
- Private Subnet

Đồng thời tìm hiểu ý nghĩa của CIDR Block trong việc phân chia địa chỉ IP.

Ví dụ:

- Public Subnet: **10.0.1.0/24**
- Private Subnet: **10.0.2.0/24**

> **Chèn hình:** VPC gồm nhiều Subnet.

---

# 3.4 Tạo Public Subnet

Tôi tiến hành tạo Public Subnet.

Các bước thực hiện:

VPC → Subnets → Create Subnet

Sau đó cấu hình:

- VPC
- Availability Zone
- CIDR Block

Sau khi tạo thành công, Public Subnet sẽ được sử dụng để triển khai các tài nguyên có thể truy cập từ Internet.

Ví dụ:

- Web Server
- Bastion Host

> **Chèn hình:** Tạo Public Subnet.

---

# 3.5 Tạo Private Subnet

Tiếp theo, tôi tạo Private Subnet.

Private Subnet được sử dụng để triển khai các dịch vụ không cần truy cập trực tiếp từ Internet.

Ví dụ:

- Database
- Backend Server
- Internal Service

Thông qua nội dung này, tôi hiểu được lý do nên tách biệt các tài nguyên quan trọng khỏi Internet nhằm tăng cường bảo mật.

> **Chèn hình:** Tạo Private Subnet.

---

# 3.6 Tìm hiểu Internet Gateway

Internet Gateway (IGW) là thành phần cho phép các tài nguyên trong Public Subnet có thể giao tiếp với Internet.

Tôi thực hiện:

VPC → Internet Gateway → Create

Sau đó:

- Tạo Internet Gateway.
- Attach Internet Gateway vào VPC.

Sau khi hoàn thành, VPC đã có khả năng kết nối Internet.

> **Chèn hình:** Attach Internet Gateway.

---

# 3.7 Cấu hình Route Table

Tiếp theo, tôi tìm hiểu Route Table.

Route Table quy định đường đi của các gói tin trong hệ thống mạng.

Tôi thực hiện:

- Tạo Route Table.
- Liên kết Route Table với Public Subnet.
- Thêm Route:

```
Destination: 0.0.0.0/0

Target:

Internet Gateway
```

Sau khi cấu hình, các EC2 trong Public Subnet có thể truy cập Internet.

> **Chèn hình:** Route Table.

---

# 3.8 Tìm hiểu NAT Gateway

Sau khi Public Subnet hoạt động, tôi tiếp tục nghiên cứu NAT Gateway.

NAT Gateway cho phép các tài nguyên trong Private Subnet truy cập Internet để:

- Cập nhật hệ điều hành.
- Tải package.
- Gọi API bên ngoài.

Trong khi đó, các thiết bị từ Internet vẫn không thể truy cập trực tiếp vào Private Subnet.

Tôi tìm hiểu:

- Elastic IP
- NAT Gateway
- Private Route Table

Thông qua nội dung này, tôi hiểu được vai trò của NAT Gateway trong việc tăng cường bảo mật cho hệ thống.

> **Chèn hình:** NAT Gateway.

---

# 3.9 Tìm hiểu Security Group

Tiếp theo, tôi nghiên cứu Security Group.

Security Group hoạt động như Firewall của từng tài nguyên AWS.

Tôi thực hành:

- Tạo Security Group.
- Thêm Inbound Rule.
- Thêm Outbound Rule.

Ví dụ:

Inbound:

- SSH (22)
- HTTP (80)
- HTTPS (443)

Qua nội dung này, tôi hiểu được nguyên tắc chỉ mở các cổng cần thiết nhằm giảm thiểu nguy cơ tấn công.

> **Chèn hình:** Security Group.

---

# 3.10 Tìm hiểu Network ACL

Ngoài Security Group, tôi còn tìm hiểu Network Access Control List (Network ACL).

Khác với Security Group:

- Security Group hoạt động ở cấp Instance.
- Network ACL hoạt động ở cấp Subnet.

Tôi tìm hiểu:

- Inbound Rule
- Outbound Rule
- Rule Number
- Allow
- Deny

Qua đó, tôi hiểu được cách kết hợp Security Group và Network ACL để xây dựng nhiều lớp bảo mật cho hệ thống.

> **Chèn hình:** Network ACL.

---

# 3.11 Thiết kế kiến trúc mạng

Sau khi hoàn thành các nội dung trên, tôi tiến hành thiết kế mô hình mạng phục vụ cho dự án.

Kiến trúc gồm:

- 01 VPC
- 02 Availability Zone
- Public Subnet
- Private Subnet
- Internet Gateway
- NAT Gateway
- Route Table
- Security Group

Đây là mô hình mạng phổ biến khi triển khai ứng dụng trên AWS.

> **Chèn hình:** Sơ đồ kiến trúc VPC của dự án.

---

# 3.12 Khó khăn gặp phải

Trong quá trình học, tôi gặp khó khăn trong việc hình dung luồng truyền dữ liệu giữa các thành phần như VPC, Subnet, Route Table, Internet Gateway và NAT Gateway.

Ngoài ra, việc phân biệt chức năng giữa Security Group và Network ACL cũng gây nhầm lẫn do cả hai đều liên quan đến kiểm soát lưu lượng mạng.

---

# 3.13 Cách giải quyết

Để khắc phục những khó khăn trên, tôi xây dựng sơ đồ kiến trúc mạng và thực hành tạo các thành phần trực tiếp trên AWS Console.

Bên cạnh đó, tôi sử dụng các sơ đồ minh họa để theo dõi đường đi của gói tin từ Internet vào VPC và giữa các Subnet. Việc kết hợp giữa lý thuyết và thực hành giúp tôi hiểu rõ hơn vai trò của từng thành phần trong hệ thống mạng.

---

# 3.14 Kiến thức đạt được

Sau tuần thứ ba, tôi đã:

- Hiểu kiến trúc mạng trên AWS.
- Biết cách tạo và cấu hình Amazon VPC.
- Hiểu cơ chế hoạt động của Public Subnet và Private Subnet.
- Biết cách cấu hình Internet Gateway và Route Table.
- Hiểu vai trò của NAT Gateway.
- Phân biệt Security Group và Network ACL.
- Thiết kế được mô hình mạng cơ bản phục vụ triển khai ứng dụng trên AWS.

---

# 3.15 Đánh giá của bản thân

Tuần thứ ba là một trong những nội dung quan trọng nhất trong quá trình học AWS vì giúp tôi hiểu rõ nền tảng mạng của các dịch vụ Cloud. Mặc dù ban đầu các khái niệm như VPC, Route Table, NAT Gateway và Network ACL khá phức tạp, nhưng sau khi thực hành trực tiếp trên AWS Console và tự thiết kế sơ đồ kiến trúc mạng, tôi đã nắm được nguyên lý hoạt động của chúng.

Những kiến thức đạt được trong tuần này là cơ sở để tôi tiếp tục triển khai các dịch vụ Serverless như AWS Lambda, Amazon API Gateway và Amazon Cognito trong các tuần tiếp theo.