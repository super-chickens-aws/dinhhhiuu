+++
title = "1.1 Tuần 1 - Làm quen với AWS Cloud"
weight = 1

[params]
  collapsibleMenu = true
+++

## Mục tiêu

Trong tuần đầu tiên, tôi làm quen với chương trình thực tập và nền tảng Amazon Web Services (AWS). Mục tiêu của tuần này là hiểu các kiến thức nền tảng về điện toán đám mây, kiến trúc hạ tầng AWS, cách quản lý tài khoản và phân quyền người dùng, đồng thời thiết lập môi trường làm việc phục vụ cho các tuần tiếp theo.

---

## 1. Tìm hiểu chương trình thực tập

Trong buổi đầu tiên, tôi xác định các vấn đè:

- Đơn vị thực tập.
- Nội dung đào tạo trong 08 tuần.
- Dự án sẽ thực hiện.
- Các tiêu chí đánh giá.
- Các dịch vụ AWS sẽ sử dụng.

Lộ trình học được chia thành hai giai đoạn:

- Giai đoạn 1: Học các dịch vụ nền tảng của AWS.
- Giai đoạn 2: Xây dựng ứng dụng Text-to-Speech theo kiến trúc Serverless.

---

## 2. Tìm hiểu Cloud Computing

Đầu tiên, tôi tìm hiểu khái niệm **Cloud Computing**.

Cloud Computing là mô hình cung cấp tài nguyên công nghệ thông tin thông qua Internet, cho phép người dùng sử dụng máy chủ, lưu trữ, cơ sở dữ liệu, mạng và nhiều dịch vụ khác mà không cần đầu tư hoặc quản lý hạ tầng phần cứng trực tiếp.

Trong quá trình học, tôi nghiên cứu các mô hình triển khai của Cloud Computing, bao gồm:

- Public Cloud
- Private Cloud
- Hybrid Cloud

Bên cạnh đó, tôi cũng tìm hiểu ba mô hình dịch vụ phổ biến:

- Infrastructure as a Service (IaaS)
- Platform as a Service (PaaS)
- Software as a Service (SaaS)

Thông qua các kiến thức trên, tôi hiểu được những lợi ích mà Cloud Computing mang lại và lý do nhiều doanh nghiệp đang chuyển đổi từ hạ tầng truyền thống (On-premises) sang mô hình điện toán đám mây.

### So sánh giữa On-premises và Cloud Computing

| Tiêu chí | On-premises | Cloud Computing |
|----------|-------------|-----------------|
| Hạ tầng | Do doanh nghiệp tự đầu tư và quản lý | Do nhà cung cấp Cloud quản lý |
| Chi phí ban đầu | Cao, cần đầu tư máy chủ và thiết bị | Thấp, trả phí theo mức sử dụng |
| Khả năng mở rộng | Khó mở rộng, cần bổ sung phần cứng | Mở rộng hoặc thu hẹp tài nguyên nhanh chóng |
| Thời gian triển khai | Có thể mất nhiều ngày hoặc nhiều tuần | Chỉ mất vài phút để khởi tạo tài nguyên |
| Bảo trì | Do doanh nghiệp tự bảo trì và nâng cấp | Nhà cung cấp Cloud chịu trách nhiệm bảo trì hạ tầng |
| Khả năng truy cập | Chủ yếu trong mạng nội bộ hoặc qua VPN | Truy cập từ Internet với quyền phù hợp |
| Tính sẵn sàng | Phụ thuộc vào hạ tầng của doanh nghiệp | Được thiết kế với tính sẵn sàng và độ tin cậy cao |
| Ví dụ | Máy chủ đặt tại công ty | Amazon Web Services (AWS), Microsoft Azure, Google Cloud Platform |

---

## 3. Tìm hiểu AWS Global Infrastructure

Sau khi hiểu Cloud Computing, tôi tiếp tục tìm hiểu hạ tầng toàn cầu của AWS.

Các nội dung nghiên cứu gồm:

### Region

Region là khu vực địa lý nơi AWS triển khai các trung tâm dữ liệu.

Ví dụ:

- Singapore
- Tokyo
- Virginia

Tôi tìm hiểu cách lựa chọn Region phù hợp với người dùng nhằm giảm độ trễ và đáp ứng yêu cầu về dữ liệu.

---

### Availability Zone

Mỗi Region bao gồm nhiều Availability Zone.

Các Availability Zone hoạt động độc lập nhưng vẫn có kết nối tốc độ cao với nhau.

Việc triển khai hệ thống trên nhiều Availability Zone giúp:

- Tăng tính sẵn sàng.
- Tăng khả năng chịu lỗi.
- Hạn chế gián đoạn dịch vụ.

---

### Edge Location

Edge Location là các điểm phân phối nội dung của AWS.

Tôi tìm hiểu Edge Location được sử dụng trong:

- Amazon CloudFront
- Amazon Route 53

Nhằm giảm thời gian phản hồi cho người dùng ở nhiều khu vực khác nhau.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog1.webp)

---

## 4. Tìm hiểu AWS IAM

Sau khi nắm được kiến trúc AWS, tôi bắt đầu tìm hiểu dịch vụ AWS Identity and Access Management (IAM).

IAM cho phép quản lý:

- Người dùng.
- Nhóm người dùng.
- Quyền truy cập.
- Vai trò của từng dịch vụ.

Trong doanh nghiệp, Root User hầu như không được sử dụng cho các công việc hằng ngày.

Thay vào đó, mỗi nhân viên sẽ có một IAM User riêng với các quyền phù hợp.

---

### 4.1 Tạo IAM User

Đầu tiên, truy cập:

**IAM → Users → Create User**

Sau đó thực hiện:

- Nhập tên người dùng.
- Chọn cho phép đăng nhập AWS Management Console.
- Thiết lập mật khẩu.

Sau khi tạo thành công, AWS cung cấp đường dẫn đăng nhập dành riêng cho IAM User.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog2.png)

---

### 4.2 Gán quyền cho IAM User

Tiếp theo, tôi tiến hành cấp quyền cho người dùng.

Các bước thực hiện: **IAM → Users → Permissions → Add permissions**

Tôi lựa chọn: **Attach policies directly**

Sau đó tìm kiếm: **AdministratorAccess**

Gán cho người dùng.

Sau khi hoàn thành, IAM User có thể sử dụng hầu hết các dịch vụ AWS.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog3.png)

---

### 4.3 Đăng nhập bằng IAM User

Sau khi tạo tài khoản, tôi đăng xuất khỏi Root User.

Tiếp theo:

- Truy cập đường dẫn đăng nhập IAM.
- Nhập Account ID.
- Nhập Username.
- Nhập Password.

Đăng nhập thành công bằng IAM User.

Qua đó, tôi hiểu được quy trình quản lý tài khoản trong doanh nghiệp.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog4.png)

---

### 4.4 Tìm hiểu IAM Policy

Tiếp theo, tôi nghiên cứu IAM Policy.

IAM Policy là tập hợp các quyền dưới dạng tài liệu JSON.

Policy quy định:

- Được phép thao tác gì.
- Không được phép thao tác gì.
- Được phép thao tác trên tài nguyên nào.

Tôi mở một số Policy có sẵn của AWS để quan sát cấu trúc JSON và hiểu cách AWS quản lý quyền truy cập.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog5.png)

---

### 4.5 Tìm hiểu IAM Role

Ngoài User và Policy, tôi tiếp tục tìm hiểu IAM Role.

IAM Role không gắn với người dùng mà được cấp cho dịch vụ AWS.

Ví dụ:

- EC2 truy cập S3.
- Lambda truy cập DynamoDB.
- Lambda gọi Amazon Polly.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog6.png)

Qua nội dung này, tôi hiểu được lý do các dịch vụ AWS có thể giao tiếp với nhau mà không cần lưu trữ Access Key trong mã nguồn.

---

## 5. Thiết lập AWS CLI

AWS Command Line Interface (AWS CLI) là công cụ do Amazon Web Services cung cấp, cho phép quản lý và thao tác với các dịch vụ AWS thông qua dòng lệnh. Trong dự án, AWS CLI được sử dụng để xác thực tài khoản AWS và hỗ trợ quá trình phát triển, triển khai ứng dụng. 

---

### 5.1 Cài đặt AWS CLI

Đầu tiên, tôi tải bộ cài AWS CLI dành cho hệ điều hành Windows tại địa chỉ:

**https://awscli.amazonaws.com/AWSCLIV2.msi**

Sau khi tải về, mở tệp `AWSCLIV2.msi` và tiến hành cài đặt.

Các bước thực hiện:

- Chọn **Next**.
- Chọn **Next**.
- Chọn **Install**.
- Chờ quá trình cài đặt hoàn tất.
- Chọn **Finish** để kết thúc.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog7.png)

---

### 5.2 Kiểm tra cài đặt

Sau khi cài đặt, mở **Command Prompt** hoặc **PowerShell** và thực hiện lệnh:

```bash
aws --version
```

Nếu cài đặt thành công, màn hình sẽ hiển thị thông tin tương tự:

```text
aws-cli/2.xx.x Python/3.xx Windows/11 exe/AMD64
```

Kết quả trên cho thấy AWS CLI đã được cài đặt thành công.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog8.png)

---

### 5.3 Tạo Access Key

Để AWS CLI có thể truy cập vào tài khoản AWS, cần tạo **Access Key** cho IAM User.

Thực hiện theo các bước sau:

- Đăng nhập **AWS Management Console**.
- Chọn **IAM**.
- Chọn **Users**.
- Chọn IAM User đã tạo.
- Chọn tab **Security credentials**.
- Kéo xuống mục **Access keys**.
- Chọn **Create access key**.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog9.png)

Tại màn hình **Use case**, chọn:

- **Command Line Interface (CLI)**

Đánh dấu xác nhận:

- **I understand the above recommendation and want to proceed to create an access key.**

Sau đó chọn:

- **Next**
- **Create access key**

AWS sẽ cung cấp hai thông tin:

- **Access Key ID**
- **Secret Access Key**

Có thể chọn **Download .csv file** để lưu lại hai thông tin này.

> **Lưu ý:** Secret Access Key chỉ hiển thị **một lần**. Nếu làm mất, cần tạo Access Key mới.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog10.png)

---

### 5.4 Cấu hình AWS CLI

Mở **Command Prompt** hoặc **PowerShell**, sau đó thực hiện lệnh:

```bash
aws configure
```

Lần lượt nhập các thông tin:

```text
AWS Access Key ID:
```

Nhập **Access Key ID** vừa tạo.

```text
AWS Secret Access Key:
```

Nhập **Secret Access Key**.

```text
Default region name:
```

Ví dụ:

```text
ap-southeast-1
```

```text
Default output format:
```

Nhập:

```text
json
```

Sau khi hoàn tất, AWS CLI sẽ tự động lưu các thông tin cấu hình trên máy tính.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog1png)

---

### 5.5 Kiểm tra kết nối

Để kiểm tra AWS CLI đã được cấu hình chính xác, thực hiện lệnh:

```bash
aws sts get-caller-identity
```

Nếu cấu hình thành công, màn hình sẽ hiển thị kết quả tương tự:

```json
{
  "UserId": "AIDAXXXXXXXXXXXXX",
  "Account": "123456789012",
  "Arn": "arn:aws:iam::123456789012:user/aws-user"
}
```

Thông tin trả về bao gồm:

- **UserId:** Định danh của IAM User.
- **Account:** Mã tài khoản AWS.
- **Arn:** Amazon Resource Name (ARN) của IAM User.

Việc hiển thị các thông tin trên chứng tỏ AWS CLI đã kết nối thành công với tài khoản AWS và sẵn sàng sử dụng để quản lý các dịch vụ AWS.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog12.png)


---

### 5.6 Kết quả

Sau khi hoàn thành các bước trên, AWS CLI đã được cài đặt và cấu hình thành công. Môi trường phát triển đã sẵn sàng để tương tác với các dịch vụ AWS thông qua dòng lệnh, phục vụ cho quá trình triển khai và quản lý tài nguyên trong các phần tiếp theo của dự án.

---

## 6. Khó khăn gặp phải

Trong tuần đầu tiên, tôi gặp khó khăn trong việc phân biệt các thành phần của AWS Global Infrastructure và cách IAM quản lý quyền truy cập.

Ngoài ra, số lượng dịch vụ của AWS rất lớn nên việc ghi nhớ chức năng của từng dịch vụ cần nhiều thời gian.

---

## 7. Cách giải quyết

Để khắc phục các khó khăn trên, tôi:

- Đọc tài liệu AWS Documentation.
- Xem video hướng dẫn.
- Thực hành trực tiếp trên AWS Console.
- Ghi chú các khái niệm quan trọng.
- Vẽ sơ đồ tổng hợp kiến thức.

Việc kết hợp giữa lý thuyết và thực hành giúp tôi hiểu rõ hơn cách AWS vận hành.

---

## 8. Kiến thức đạt được

Sau tuần đầu tiên, tôi đã:

- Hiểu Cloud Computing.
- Hiểu AWS Global Infrastructure.
- Thành thạo thao tác trên AWS Console.
- Tạo và quản lý IAM User.
- Gán Policy.
- Hiểu nguyên lý hoạt động của IAM Role.
- Chuẩn bị đầy đủ môi trường phát triển.

---

## 9. Đánh giá của bản thân

Tuần đầu tiên giúp tôi xây dựng nền tảng kiến thức về AWS và tạo tiền đề cho các nội dung chuyên sâu trong những tuần tiếp theo. Việc được trực tiếp thao tác trên AWS Console giúp tôi hiểu rõ hơn cách quản lý tài nguyên và các nguyên tắc bảo mật khi làm việc với nền tảng Cloud.

Trong thời gian tới, tôi sẽ tiếp tục nghiên cứu các dịch vụ như Amazon EC2, Amazon S3 và Amazon VPC để từng bước xây dựng ứng dụng theo kiến trúc Serverless.