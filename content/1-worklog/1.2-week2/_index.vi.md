+++
title = "1.2 Tuần 2 - Làm quen với Amazon EC2 và Amazon S3"
weight = 2

[params]
  collapsibleMenu = true
+++

## Mục tiêu

Trong tuần thứ hai, tôi tìm hiểu hai dịch vụ nền tảng của Amazon Web Services là Amazon EC2 và Amazon S3. Mục tiêu của tuần học là hiểu cách triển khai máy chủ trên nền tảng Cloud, quản lý tài nguyên tính toán, lưu trữ dữ liệu và làm quen với các cơ chế bảo mật cơ bản khi triển khai hệ thống.

---

## 1. Tìm hiểu Amazon EC2

Amazon Elastic Compute Cloud (Amazon EC2) là dịch vụ cung cấp máy chủ ảo trên nền tảng Amazon Web Services (AWS). Dịch vụ này cho phép người dùng nhanh chóng khởi tạo, cấu hình và quản lý các máy chủ phục vụ cho việc triển khai ứng dụng mà không cần đầu tư hạ tầng phần cứng.

So với máy chủ truyền thống, Amazon EC2 có ưu điểm là khả năng mở rộng linh hoạt, thời gian triển khai nhanh và mô hình thanh toán theo mức sử dụng.

Trong quá trình tìm hiểu, tôi nghiên cứu các thành phần chính của Amazon EC2 như sau:

| Thành phần | Mô tả |
|------------|-------|
| **Instance** | Là một máy chủ ảo được tạo trên AWS. Mỗi Instance có hệ điều hành, CPU, RAM, ổ đĩa và địa chỉ IP riêng để chạy ứng dụng. |
| **Instance Type** | Xác định cấu hình phần cứng của Instance như số lượng CPU, dung lượng RAM, băng thông mạng và mục đích sử dụng (General Purpose, Compute Optimized, Memory Optimized,...). |
| **Amazon Machine Image (AMI)** | Là mẫu hệ điều hành đã được cấu hình sẵn, bao gồm hệ điều hành và các phần mềm cần thiết. Khi tạo Instance, người dùng lựa chọn một AMI để làm nền tảng khởi tạo máy chủ. |
| **Key Pair** | Cặp khóa gồm Public Key và Private Key dùng để xác thực khi kết nối đến EC2. Private Key được lưu trên máy người dùng và được sử dụng để đăng nhập thông qua SSH hoặc Remote Desktop. |
| **Security Group** | Hoạt động như tường lửa ảo (Virtual Firewall), cho phép cấu hình các quy tắc truy cập vào và ra khỏi EC2 theo địa chỉ IP, giao thức và cổng (Port). |
| **Elastic IP** | Địa chỉ IPv4 tĩnh có thể gán cho EC2. Elastic IP giúp địa chỉ IP của máy chủ không thay đổi khi khởi động lại hoặc thay thế Instance. |

Qua việc tìm hiểu các thành phần trên, tôi hiểu được quy trình triển khai một máy chủ trên nền tảng AWS, từ việc lựa chọn hệ điều hành, cấu hình phần cứng, thiết lập bảo mật đến kết nối và quản lý máy chủ.

### Mối quan hệ giữa các thành phần

Quá trình khởi tạo một EC2 Instance có thể được mô tả như sau:


![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog13.png)

Sơ đồ trên cho thấy, để tạo một EC2 Instance cần lựa chọn AMI và Instance Type trước. Sau đó cấu hình Key Pair để đăng nhập vào máy chủ, Security Group để kiểm soát truy cập và có thể gán thêm Elastic IP nếu cần sử dụng địa chỉ IP tĩnh.

---

## 2. Thực hành tạo Amazon EC2 Instance

Sau khi tìm hiểu các khái niệm cơ bản về Amazon EC2, tôi tiến hành tạo một máy chủ ảo đầu tiên trên nền tảng AWS.

Đăng nhập vào **AWS Management Console**, sau đó chọn:

**Amazon EC2 → Instances → Launch instances**

Tại màn hình **Launch an instance**, tiến hành cấu hình các thông tin sau.

---

### 2.1 Đặt tên EC2 Instance

Trong mục **Name and tags**, nhập tên cho máy chủ.

Ví dụ:

```text
tts-server
```

Việc đặt tên giúp dễ dàng nhận biết và quản lý EC2 Instance trong quá trình phát triển.

---

### 2.2 Chọn Amazon Machine Image (AMI)

Trong mục **Application and OS Images (Amazon Machine Image)**, lựa chọn:

```text
Amazon Linux 2023 AMI
```

Amazon Linux là hệ điều hành do AWS phát triển và tối ưu cho các dịch vụ trên nền tảng AWS, đồng thời thường xuyên được cập nhật về hiệu năng và bảo mật.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog14.png)

---

### 2.3 Chọn Instance Type

Trong mục **Instance type**, lựa chọn:

```text
t2.micro
```

Đây là cấu hình thuộc **AWS Free Tier**, phù hợp cho việc học tập và triển khai các ứng dụng nhỏ.

Thông số cơ bản:

- 1 vCPU
- 1 GB RAM

---

### 2.4 Tạo Key Pair

Trong mục **Key pair (login)**, chọn:

**Create new key pair**

Sau đó cấu hình:

| Thuộc tính | Giá trị |
|------------|----------|
| Key pair name | `tts-key` |
| Key pair type | RSA |
| Private key file format | `.pem` |

Nhấn **Create key pair**.

Trình duyệt sẽ tự động tải về tệp:

```text
tts-key.pem
```

Đây là khóa dùng để xác thực khi kết nối tới EC2 thông qua SSH.

> **Lưu ý:** Tệp `.pem` chỉ được tải xuống một lần. Nếu làm mất, cần tạo Key Pair mới.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog15.png)

---

### 2.5 Cấu hình Network Settings

Trong phần **Network settings**, chọn **Edit** để chỉnh sửa cấu hình.

Thiết lập như sau:

- Auto-assign Public IP: **Enable**
- Firewall (security groups): **Create security group**

Cấu hình các quy tắc truy cập:

| Type | Port | Source | Mục đích |
|------|------|--------|----------|
| SSH | 22 | My IP | Cho phép kết nối SSH từ máy tính cá nhân |
| HTTP | 80 | Anywhere | Cho phép truy cập Web |
| HTTPS | 443 | Anywhere | Cho phép truy cập HTTPS |

Đối với quá trình học tập, cổng **SSH** chỉ mở cho địa chỉ IP của máy tính hiện tại nhằm tăng tính bảo mật.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog16.png)


![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog17.png)

---

### 2.6 Khởi tạo EC2 Instance

Sau khi hoàn tất cấu hình, chọn:

**Launch Instance**

AWS sẽ tiến hành khởi tạo EC2 Instance.

Sau khoảng vài chục giây, trạng thái của EC2 chuyển sang:

```text
Running
```

Điều này cho thấy máy chủ đã được tạo thành công.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog18.png)

---

## 3 Kết nối tới EC2 bằng Windows Terminal

Sau khi EC2 Instance hoạt động, tôi tiến hành kết nối đến máy chủ thông qua giao thức **SSH (Secure Shell)** bằng **Windows Terminal**.

---

### 3.1 Chuẩn bị thông tin kết nối

Đầu tiên, truy cập:

**Amazon EC2 → Instances**

Chọn EC2 vừa tạo và tại mục **Details**, ghi lại:

- Public IPv4 Address
- Public IPv4 DNS (nếu cần)

Ví dụ:

```text
13.212.xxx.xxx
```

Đồng thời chuẩn bị tệp:

```text
tts-key.pem
```

đã được tải về khi tạo Key Pair.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog19.png)


---

### 3.2 Mở Windows Terminal

Mở **Windows Terminal** hoặc **PowerShell**.

Di chuyển đến thư mục chứa tệp `.pem`.

Ví dụ, nếu tệp nằm trong thư mục **Downloads**:

```powershell
cd $HOME\Downloads
```

Kiểm tra tệp đã tồn tại:

```powershell
dir
```

Kết quả sẽ hiển thị:

```text
tts-key.pem
```

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog20.png)


---

### 3.3 Kết nối tới EC2

Thực hiện lệnh:

```bash
ssh -i tts-key.pem ec2-user@13.212.xxx.xxx
```

Trong đó:

- `-i` chỉ định tệp Key Pair.
- `tts-key.pem` là tệp khóa được AWS cung cấp.
- `ec2-user` là tài khoản mặc định của Amazon Linux.
- `13.212.xxx.xxx` là địa chỉ Public IP của EC2.

Lần đầu kết nối, Terminal sẽ hiển thị thông báo:

```text
The authenticity of host '13.212.xxx.xxx' can't be established.
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

Nhập:

```text
yes
```

và nhấn **Enter**.

{{% notice style="warning" title="Lưu ý đối với Windows" icon="triangle-exclamation" %}}

Nếu sử dụng **Windows Terminal** và gặp thông báo:

```text
Permissions for 'tts-key.pem' are too open.
This private key will be ignored.
```

Nguyên nhân là tệp **`.pem`** đang được cấp quyền truy cập quá rộng. Trước khi kết nối bằng SSH, cần giới hạn quyền truy cập của tệp khóa.

Các bước thực hiện:

1. Chuột phải vào tệp **`tts-key.pem`** → **Properties**.
2. Chọn tab **Security** → **Advanced**.
3. Chọn **Disable inheritance**.
4. Chọn **Convert inherited permissions into explicit permissions**.
5. Xóa quyền của nhóm **Users**, chỉ giữ lại quyền của tài khoản Windows hiện tại (và **SYSTEM**, **Administrators** nếu cần).
6. Nhấn **Apply** và **OK** để lưu thay đổi.

Sau khi hoàn thành, tiếp tục thực hiện lệnh SSH.

{{% /notice %}}

Nếu kết nối thành công, màn hình sẽ hiển thị giao diện Terminal của Amazon Linux.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog21.png)

---

### 3.4 Kiểm tra EC2

Sau khi đăng nhập thành công, tôi thực hiện một số lệnh để kiểm tra trạng thái của máy chủ.

Kiểm tra người dùng hiện tại:

```bash
whoami
```

Kiểm tra hệ điều hành:

```bash
cat /etc/os-release
```

Kiểm tra tên máy chủ:

```bash
hostname
```

Kiểm tra dung lượng ổ đĩa:

```bash
df -h
```

Kiểm tra bộ nhớ RAM:

```bash
free -h
```

Kiểm tra địa chỉ IP:

```bash
hostname -I
```

Thông qua các lệnh trên, tôi xác nhận EC2 Instance đã hoạt động bình thường và sẵn sàng cho việc cài đặt phần mềm hoặc triển khai ứng dụng.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog22.png)

---

### 3.5 Kết quả

Sau khi hoàn thành các bước trên, tôi đã tạo thành công một Amazon EC2 Instance và kết nối tới máy chủ bằng Windows Terminal thông qua giao thức SSH. Đồng thời, tôi làm quen với các thao tác quản trị Linux cơ bản như kiểm tra hệ điều hành, dung lượng ổ đĩa, bộ nhớ và địa chỉ IP, tạo nền tảng cho việc triển khai ứng dụng trên môi trường Cloud ở các nội dung tiếp theo.

## 4. Quản lý EC2 Instance

Tiếp theo, tôi thực hành quản lý vòng đời của EC2 Instance.

Bao gồm:

- Start Instance
- Stop Instance
- Reboot Instance
- Terminate Instance

Qua đó, tôi hiểu được sự khác nhau giữa việc dừng, khởi động lại và xóa hoàn toàn một máy chủ.

---

## 5. Tìm hiểu Amazon S3

Sau khi hoàn thành nội dung EC2, tôi tiếp tục tìm hiểu Amazon Simple Storage Service (Amazon S3).

Amazon S3 là dịch vụ lưu trữ đối tượng (Object Storage) của AWS.

Các dữ liệu được lưu dưới dạng:

- Bucket
- Object

Amazon S3 có khả năng lưu trữ dung lượng rất lớn với độ bền dữ liệu cao và được sử dụng phổ biến trong việc lưu trữ hình ảnh, video, tài liệu và các tệp tĩnh.

---

## 6. Thực hành tạo Amazon S3 Bucket

Sau khi tìm hiểu về dịch vụ Amazon S3, tôi tiến hành tạo Bucket đầu tiên để lưu trữ dữ liệu trên nền tảng AWS.

Đăng nhập vào **AWS Management Console**, sau đó chọn:

**Amazon S3 → Buckets → Create bucket**

---

### 6.1 Đặt tên Bucket

Trong mục **Bucket name**, nhập tên Bucket.

Ví dụ:

```text
tts-storage-demo
```

Tên Bucket phải thỏa mãn các yêu cầu sau:

- Chỉ chứa chữ thường (`a-z`), số (`0-9`) và dấu gạch ngang (`-`).
- Không chứa khoảng trắng hoặc ký tự đặc biệt.
- Phải là duy nhất trên toàn bộ hệ thống Amazon S3.

---

### 6.2 Cấu hình Block Public Access

Amazon S3 mặc định sẽ chặn toàn bộ truy cập công khai để đảm bảo an toàn dữ liệu.

Trong quá trình thực hành, tôi giữ nguyên thiết lập mặc định:

```text
Block all public access
```

Điều này giúp Bucket chỉ có thể được truy cập bởi những người hoặc dịch vụ đã được cấp quyền.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog23.png)

---

### 6.3 Tạo Bucket

Sau khi hoàn tất cấu hình, chọn:

**Create bucket**

Bucket mới sẽ xuất hiện trong danh sách Buckets và sẵn sàng để lưu trữ dữ liệu.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog24.png)


---

## 6.4 Upload dữ liệu lên Amazon S3

Sau khi tạo Bucket, tôi tiến hành tải dữ liệu lên Amazon S3 để tìm hiểu cách lưu trữ theo mô hình Object Storage.

Đầu tiên, truy cập vào Bucket vừa tạo, sau đó chọn:

**Upload → Add files**

Tiến hành chọn một số tệp để tải lên, bao gồm:

- Hình ảnh (`.png`, `.jpg`)
- Tài liệu (`.pdf`)
- Trang Web tĩnh (`.html`)

Sau khi chọn tệp, nhấn:

**Upload**

Amazon S3 sẽ lưu từng tệp dưới dạng một **Object**.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog25.png)

---

### 6.5 Kiểm tra Object

Sau khi Upload hoàn tất, mỗi tệp sẽ xuất hiện trong Bucket với các thông tin như:

| Thuộc tính | Ý nghĩa |
|------------|----------|
| Object Key | Tên định danh của Object trong Bucket |
| Size | Kích thước tệp |
| Last Modified | Thời điểm tải lên |
| Storage Class | Lớp lưu trữ đang sử dụng |

Qua quá trình thực hành, tôi hiểu rằng Amazon S3 không quản lý dữ liệu theo thư mục như hệ điều hành thông thường. Mỗi tệp được lưu dưới dạng một **Object**, được định danh bằng **Object Key**.

---

### 6.6 Tìm hiểu Storage Class

Amazon S3 hỗ trợ nhiều lớp lưu trữ khác nhau nhằm tối ưu chi phí và hiệu năng.

Trong quá trình thực hành, tôi sử dụng lớp lưu trữ mặc định:

```text
S3 Standard
```

Đây là lớp lưu trữ phù hợp với dữ liệu thường xuyên được truy cập.

Ngoài ra, tôi tìm hiểu thêm một số Storage Class khác:

| Storage Class | Mục đích |
|---------------|----------|
| S3 Standard | Dữ liệu truy cập thường xuyên |
| S3 Intelligent-Tiering | Tự động tối ưu chi phí |
| S3 Standard-IA | Dữ liệu ít truy cập |
| S3 Glacier Instant Retrieval | Lưu trữ lâu dài nhưng vẫn cần truy cập nhanh |
| S3 Glacier Flexible Retrieval | Sao lưu và lưu trữ dài hạn |
| S3 Glacier Deep Archive | Lưu trữ rất dài hạn với chi phí thấp |

---

## 7. Quản lý quyền truy cập Amazon S3

Sau khi hoàn thành việc lưu trữ dữ liệu, tôi tiếp tục tìm hiểu cơ chế quản lý quyền truy cập của Amazon S3 nhằm đảm bảo an toàn cho dữ liệu.

Amazon S3 cung cấp nhiều cơ chế kiểm soát quyền khác nhau như:

- Block Public Access
- Bucket Policy
- IAM Policy
- Object ACL

---

### 7.1 Block Public Access

Đây là lớp bảo vệ đầu tiên của Amazon S3.

Mặc định, AWS sẽ bật:

```text
Block all public access
```

Điều này giúp ngăn Bucket hoặc Object bị truy cập công khai ngoài Internet.

Trong quá trình thực hành, tôi giữ nguyên cấu hình mặc định để đảm bảo an toàn dữ liệu.

---

### 7.2 Bucket Policy

Bucket Policy là tập hợp các quy tắc (JSON Policy) dùng để xác định ai được phép truy cập vào Bucket và được phép thực hiện những thao tác nào.

Ví dụ:

- Cho phép đọc dữ liệu.
- Cho phép Upload.
- Chỉ cho phép một IAM User hoặc IAM Role cụ thể truy cập.

Thông qua Bucket Policy, có thể quản lý quyền truy cập cho toàn bộ Bucket mà không cần cấu hình từng Object riêng lẻ.

---

### 7.3 Object Permission

Ngoài Bucket Policy, mỗi Object cũng có thể được thiết lập quyền truy cập riêng.

Trong quá trình thực hành, tôi tìm hiểu các thông tin như:

- Chủ sở hữu (Owner)
- Quyền truy cập (Permissions)
- Metadata của Object

Qua đó, tôi hiểu rằng quyền của từng Object có thể khác với quyền của toàn bộ Bucket nếu được cấu hình riêng.

---

### 7.4 Kết quả

Sau khi hoàn thành các nội dung trên, tôi đã tạo thành công Amazon S3 Bucket, tải dữ liệu lên Cloud và tìm hiểu các cơ chế quản lý quyền truy cập của Amazon S3. Đồng thời, tôi hiểu được vai trò của **Block Public Access**, **Bucket Policy** và **Object Permission** trong việc bảo vệ dữ liệu trên nền tảng AWS.

---

## 8. Khó khăn gặp phải

Trong quá trình thực hành, tôi gặp khó khăn khi cấu hình Security Group và kết nối SSH tới EC2 do chưa hiểu rõ các quy tắc về cổng mạng và quyền truy cập.

Ngoài ra, việc phân biệt quyền truy cập giữa Bucket Policy và Block Public Access của Amazon S3 cũng gây nhầm lẫn trong giai đoạn đầu.

---

## 9. Cách giải quyết

Để giải quyết các vấn đề trên, tôi tham khảo tài liệu chính thức của AWS, kiểm tra lại các cấu hình mạng và thực hành nhiều lần việc tạo EC2 Instance cũng như S3 Bucket.

Thông qua quá trình thử nghiệm và đối chiếu kết quả, tôi hiểu rõ hơn cơ chế bảo mật của EC2 và Amazon S3.

---

## 10. Kiến thức đạt được

Sau tuần thứ hai, tôi đã:

- Hiểu nguyên lý hoạt động của Amazon EC2.
- Thành thạo quy trình tạo và quản lý EC2 Instance.
- Biết cách cấu hình Security Group.
- Biết cách kết nối SSH tới máy chủ Linux.
- Hiểu mô hình lưu trữ của Amazon S3.
- Tạo và quản lý Bucket.
- Upload và quản lý Object.
- Hiểu cơ chế phân quyền và bảo mật của Amazon S3.

---

## 11. Đánh giá của bản thân

Tuần thứ hai giúp tôi tiếp cận trực tiếp với các dịch vụ hạ tầng của AWS thông qua việc triển khai máy chủ EC2 và lưu trữ dữ liệu trên Amazon S3. Việc được thực hành tạo, cấu hình và quản lý tài nguyên giúp tôi hiểu rõ hơn quy trình triển khai một hệ thống trên nền tảng Cloud.

Những kiến thức và kỹ năng đạt được trong tuần này là nền tảng quan trọng để tiếp tục nghiên cứu các nội dung về mạng, kiến trúc hệ thống và các dịch vụ Serverless trong những tuần tiếp theo.