+++
title = "1.3 Tuần 3 - Tìm hiểu Amazon VPC và Networking"
weight = 3

[params]
  collapsibleMenu = true
+++

## Mục tiêu

Trong tuần thứ ba, tôi tập trung nghiên cứu kiến trúc mạng trên nền tảng Amazon Web Services (AWS). Đây là một trong những nội dung quan trọng nhất vì hầu hết các dịch vụ trên AWS đều hoạt động bên trong một hệ thống mạng riêng được quản lý bởi Amazon Virtual Private Cloud (Amazon VPC).

Mục tiêu của tuần này gồm:

- Hiểu kiến trúc mạng của AWS.
- Tìm hiểu cách xây dựng Amazon VPC.
- Hiểu cách phân chia mạng bằng Subnet.
- Tìm hiểu cơ chế kết nối Internet cho VPC.
- Tìm hiểu các thành phần bảo mật trong hệ thống mạng AWS.
- Thiết kế mô hình mạng phục vụ triển khai ứng dụng.

---

## 3.1 Tìm hiểu Amazon VPC

Amazon Virtual Private Cloud (Amazon VPC) là dịch vụ cho phép người dùng tạo một mạng riêng (Virtual Network) trên nền tảng AWS để triển khai các tài nguyên như Amazon EC2, Amazon RDS hay AWS Lambda.

Có thể hiểu VPC giống như một mạng nội bộ của doanh nghiệp, trong đó người dùng hoàn toàn chủ động quyết định:

- Dải địa chỉ IP sử dụng.
- Cách chia mạng thành nhiều Subnet.
- Những tài nguyên nào được phép truy cập Internet.
- Luồng giao tiếp giữa các tài nguyên trong hệ thống.

Nhờ đó, toàn bộ hạ tầng được tách biệt với các khách hàng khác trên AWS và có thể cấu hình theo nhu cầu của từng ứng dụng.

Trong quá trình tìm hiểu, tôi nghiên cứu các thành phần chính của Amazon VPC.

| Thành phần | Chức năng |
|------------|-----------|
| VPC | Mạng riêng chứa toàn bộ tài nguyên của hệ thống |
| Subnet | Chia VPC thành nhiều vùng mạng nhỏ |
| Route Table | Định tuyến lưu lượng mạng |
| Internet Gateway | Cho phép VPC kết nối Internet |
| NAT Gateway | Cho phép Private Subnet truy cập Internet |
| Security Group | Firewall ở cấp tài nguyên |
| Network ACL | Firewall ở cấp Subnet |

Qua nội dung này, tôi hiểu rằng Amazon VPC là nền tảng của hầu hết các dịch vụ triển khai trên AWS.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog26.webp)

---

## 3.2 Thực hành tạo Amazon VPC

Sau khi tìm hiểu lý thuyết, tôi tiến hành tạo một Amazon VPC để sử dụng cho các nội dung thực hành trong tuần.

Truy cập:

**AWS Management Console → Amazon VPC → Your VPCs → Create VPC**

---

### 3.2.1 Cấu hình VPC

Tại màn hình tạo VPC, tôi tiến hành cấu hình các thông số cơ bản.

| Thuộc tính | Giá trị |
|------------|----------|
| Resources to create | VPC only |
| Name tag | demo-vpc |
| IPv4 CIDR | 10.0.0.0/16 |
| IPv6 CIDR | No IPv6 CIDR Block |
| Tenancy | Default |

Trong đó:

- **Name tag** giúp dễ dàng nhận biết VPC trong quá trình quản lý.
- **IPv4 CIDR** xác định phạm vi địa chỉ IP của toàn bộ hệ thống mạng.
- **Tenancy** để mặc định nhằm sử dụng hạ tầng chia sẻ của AWS và không phát sinh thêm chi phí.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog27.png)

---

## 3.2.2 Tìm hiểu CIDR Block

Trong quá trình tạo VPC, tôi tìm hiểu về CIDR Block.

CIDR (Classless Inter-Domain Routing) là phương pháp biểu diễn dải địa chỉ IP.

Ví dụ:

```text
10.0.0.0/16
```

Trong đó:

- `10.0.0.0` là địa chỉ mạng.
- `/16` là số bit dành cho Network.

CIDR `/16` cho phép hệ thống có tổng cộng:

```text
65.536 địa chỉ IP
```

Từ dải địa chỉ này có thể tiếp tục chia thành nhiều Subnet nhỏ hơn.

Ví dụ:

| Subnet | CIDR |
|---------|------|
| Public Subnet | 10.0.1.0/24 |
| Private Subnet | 10.0.2.0/24 |
| Private Subnet | 10.0.3.0/24 |

Qua đó, tôi hiểu rằng CIDR Block quyết định quy mô của toàn bộ hệ thống mạng.

---

## 3.2.3 Tạo VPC

Sau khi hoàn tất cấu hình, tôi chọn:

**Create VPC**

Chỉ sau vài giây, AWS tạo thành công một VPC mới.

Tại giao diện quản lý, tôi kiểm tra các thông tin:

- VPC ID
- State
- IPv4 CIDR
- Default Route Table
- Default Network ACL

Thông qua quá trình thực hành, tôi nhận thấy mỗi VPC mới đều được AWS tự động tạo sẵn một Route Table và một Network ACL mặc định.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog28.png)

---

## 3.3 Tìm hiểu Subnet

Sau khi tạo VPC, tôi tiếp tục nghiên cứu Subnet.

Subnet là một phần mạng nhỏ được tách ra từ VPC nhằm phục vụ các mục đích triển khai khác nhau.

Một VPC có thể chứa nhiều Subnet và mỗi Subnet chỉ thuộc về một Availability Zone.

Việc chia nhỏ hệ thống thành nhiều Subnet giúp:

- Tăng khả năng quản lý.
- Nâng cao bảo mật.
- Dễ dàng mở rộng hệ thống.
- Phân tách các thành phần của ứng dụng.

Thông thường sẽ có hai loại Subnet.

| Loại | Mục đích |
|------|----------|
| Public Subnet | Chứa các tài nguyên cần truy cập Internet |
| Private Subnet | Chứa các tài nguyên nội bộ |

Ví dụ:

Public Subnet:

```text
10.0.1.0/24
```

Private Subnet:

```text
10.0.2.0/24
```

Qua nội dung này, tôi hiểu rằng việc phân chia Public và Private Subnet là nguyên tắc thiết kế phổ biến trong các hệ thống Cloud hiện đại.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog29.webp)

---

## 3.4 Thực hành tạo Public Subnet

Sau khi đã có VPC, tôi tiến hành tạo Public Subnet.

Truy cập: **Amazon VPC → Subnets → Create subnet**

---

### 3.4.1 Cấu hình Public Subnet

Tại màn hình tạo Subnet, tôi cấu hình như sau:

| Thuộc tính | Giá trị |
|------------|----------|
| VPC ID | demo-vpc |
| Subnet name | public-subnet-1 |
| Availability Zone | ap-southeast-1a |
| IPv4 CIDR | 10.0.1.0/24 |

Trong đó:

- VPC ID xác định Subnet sẽ thuộc VPC nào.
- Availability Zone xác định vị trí triển khai Subnet.
- CIDR Block xác định phạm vi địa chỉ IP của Subnet.

CIDR:

```text
10.0.1.0/24
```

cho phép Subnet có khoảng 256 địa chỉ IP.

---

### 3.4.2 Tạo Public Subnet

Sau khi hoàn tất cấu hình, tôi chọn:

**Create subnet**

AWS tạo thành công Public Subnet.

Tại màn hình quản lý, tôi kiểm tra:

- Subnet ID
- Availability Zone
- CIDR Block
- Available IP Address

Qua đó, tôi hiểu rằng Public Subnet chỉ thực sự có thể truy cập Internet sau khi được cấu hình Internet Gateway và Route Table.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog30.png)

---

## 3.5 Thực hành tạo Private Subnet

Bên cạnh Public Subnet, tôi tiếp tục tạo Private Subnet nhằm phục vụ triển khai các tài nguyên nội bộ.

Các bước thực hiện tương tự như Public Subnet.

Truy cập:

**Amazon VPC → Subnets → Create subnet**

Sau đó cấu hình:

| Thuộc tính | Giá trị |
|------------|----------|
| VPC ID | demo-vpc |
| Subnet name | private-subnet-1 |
| Availability Zone | ap-southeast-1a |
| IPv4 CIDR | 10.0.2.0/24 |

Sau khi hoàn tất, chọn:

**Create subnet**

AWS tạo thành công Private Subnet.

Khác với Public Subnet, Private Subnet sẽ không được kết nối trực tiếp với Internet. Các tài nguyên đặt trong Private Subnet thường là:

- Amazon RDS.
- Backend Server.
- Internal Service.
- Application Server.

Việc tách riêng các tài nguyên quan trọng vào Private Subnet giúp hạn chế nguy cơ bị truy cập trái phép từ Internet, góp phần nâng cao mức độ bảo mật của hệ thống.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog31.png)

---

## 3.6 Thực hành tạo Internet Gateway

Sau khi tạo VPC và các Subnet, tôi tiếp tục tìm hiểu Internet Gateway (IGW).

**Internet Gateway** là thành phần cho phép các tài nguyên trong Amazon VPC có thể giao tiếp với Internet. Nếu không có Internet Gateway, các EC2 trong VPC sẽ không thể truy cập Internet hoặc nhận yêu cầu từ bên ngoài.

Có thể hình dung Internet Gateway như "cổng ra vào" của toàn bộ VPC.

---

### 3.6.1 Tạo Internet Gateway

Truy cập: **Amazon VPC → Internet Gateways → Create Internet Gateway**

Sau đó cấu hình:

| Thuộc tính | Giá trị |
|------------|----------|
| Name tag | demo-igw |

Sau khi hoàn tất, chọn:

**Create Internet Gateway**

AWS sẽ tạo thành công một Internet Gateway mới.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog32.png)

---

## 3.6.2 Gắn Internet Gateway vào VPC

Sau khi Internet Gateway được tạo, cần gắn (Attach) vào VPC để VPC có thể kết nối với Internet.

Thực hiện: **Internet Gateway → Actions → Attach to VPC**

Chọn: VPC: **demo-vpc**

Sau đó chọn: **Attach Internet Gateway**

Khi trạng thái chuyển sang **Attached**, Internet Gateway đã được kết nối với VPC.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog33.png)

---

### 3.6.3 Vai trò của Internet Gateway

Internet Gateway có nhiệm vụ:

- Cho phép các tài nguyên trong Public Subnet truy cập Internet.
- Cho phép người dùng từ Internet truy cập vào các tài nguyên được cấp Public IP.
- Thực hiện NAT (Network Address Translation) giữa địa chỉ IP công cộng và địa chỉ IP riêng trong VPC.

Tuy nhiên, chỉ có Internet Gateway là chưa đủ. Muốn EC2 truy cập Internet còn phải cấu hình **Route Table**.

---

## 3.7 Thực hành cấu hình Route Table

Sau khi Internet Gateway được kết nối với VPC, tôi tiếp tục cấu hình Route Table.

**Route Table** là bảng định tuyến dùng để xác định đường đi của các gói tin trong hệ thống mạng.

Có thể hiểu Route Table giống như "bản đồ giao thông", giúp AWS biết dữ liệu cần đi đâu.

---

### 3.7.1 Tìm hiểu Route Table mặc định

Ngay khi tạo VPC, AWS sẽ tự động tạo một Route Table mặc định.

Trong Route Table này thường chỉ có một dòng:

| Destination | Target |
|-------------|--------|
| 10.0.0.0/16 | local |

Điều này có nghĩa:

Toàn bộ các tài nguyên bên trong VPC đều có thể giao tiếp với nhau.

Tuy nhiên vẫn chưa thể kết nối Internet.

---

### 3.7.2 Tạo Route tới Internet

Để Public Subnet có thể truy cập Internet, tôi thêm Route mới.

Thực hiện:

**Amazon VPC → Route Tables → Chọn Route Table → Edit routes**

Thêm Route:

| Destination | Target |
|-------------|--------|
| 0.0.0.0/0 | Internet Gateway |

Trong đó:

```text
Destination: 0.0.0.0/0
```

đại diện cho toàn bộ Internet.

Target sẽ chọn Internet Gateway vừa tạo.

Sau đó chọn:

**Save Changes**

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog34.png)

---

### 3.7.3 Liên kết Route Table với Public Subnet

Sau khi cấu hình Route, cần liên kết Route Table với Public Subnet.

Thực hiện: **Route Table → Subnet Associations → Edit**

Chọn: public-subnet-1

Sau đó lưu lại.

Kể từ thời điểm này, Public Subnet đã có đường đi tới Internet.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog35.png)

---

### 3.7.4 Kiểm tra kết quả

Sau khi cấu hình hoàn tất:

- EC2 trong Public Subnet có thể truy cập Internet.
- Có thể cài đặt phần mềm bằng yum hoặc dnf.
- Có thể tải package từ Internet.
- Có thể SSH từ máy tính cá nhân nếu Security Group cho phép.

Qua quá trình thực hành, tôi hiểu rằng:

Internet Gateway chỉ đóng vai trò là "cổng kết nối", còn Route Table mới quyết định lưu lượng mạng có được phép đi qua cổng đó hay không.

---

## 3.8 Tìm hiểu NAT Gateway

Sau khi Public Subnet hoạt động, tôi tiếp tục tìm hiểu NAT Gateway.

Trong quá trình học, tôi không triển khai NAT Gateway do dịch vụ này phát sinh chi phí ngoài AWS Free Tier, tuy nhiên tôi đã nghiên cứu nguyên lý hoạt động của nó.

NAT Gateway cho phép các tài nguyên trong Private Subnet truy cập Internet mà vẫn không bị truy cập trực tiếp từ Internet.

Ví dụ:

- Cập nhật hệ điều hành.
- Cài đặt package.
- Gọi API của AWS.
- Truy cập Internet để tải dữ liệu.

Trong khi đó: Người dùng Internet không thể SSH trực tiếp vào EC2 trong Private Subnet.

---

### 3.8.1 Nguyên lý hoạt động

Luồng dữ liệu sẽ diễn ra như sau:

```text
Internet
    │
    ▼
Internet Gateway
    │
    ▼
Public Subnet
    │
NAT Gateway
    │
    ▼
Private Subnet
```

Khi EC2 trong Private Subnet gửi yêu cầu ra Internet:

- Dữ liệu được chuyển tới NAT Gateway.
- NAT Gateway thay mặt EC2 gửi yêu cầu ra Internet.
- Phản hồi sẽ quay ngược về NAT Gateway.
- NAT Gateway chuyển tiếp dữ liệu cho EC2.

Nhờ đó:

- EC2 có thể truy cập Internet.
- Internet không thể chủ động truy cập EC2.

---

### 3.8.2 Elastic IP

Trong quá trình tìm hiểu NAT Gateway, tôi cũng nghiên cứu Elastic IP.

Elastic IP là địa chỉ IPv4 công cộng cố định do AWS cấp.

Elastic IP thường được sử dụng cho:

- NAT Gateway.
- Bastion Host.
- Các máy chủ cần địa chỉ IP cố định.

Khác với Public IP thông thường, Elastic IP sẽ không thay đổi sau khi EC2 khởi động lại.

---

## 3.9 Thực hành tìm hiểu Security Group

Sau khi hoàn thành phần kết nối mạng, tôi tiếp tục tìm hiểu Security Group.

Security Group hoạt động như Firewall của từng tài nguyên AWS.

Mỗi EC2 có thể gắn một hoặc nhiều Security Group.

Security Group chỉ cho phép các lưu lượng được khai báo đi qua, các lưu lượng khác sẽ tự động bị từ chối.

---

### 3.9.1 Tạo Security Group

Truy cập:

**Amazon EC2 → Security Groups → Create Security Group**

Sau đó cấu hình:

| Thuộc tính | Giá trị |
|------------|----------|
| Name | web-sg |
| VPC | demo-vpc |
| Description | Security Group cho Web Server |

---

## 3.9.2 Cấu hình Inbound Rule

Trong quá trình thực hành, tôi cấu hình các cổng sau:

| Port | Giao thức | Mục đích |
|------|-----------|----------|
| 22 | SSH | Quản trị máy chủ |
| 80 | HTTP | Website |
| 443 | HTTPS | Website bảo mật |

Nguồn truy cập:

- SSH: My IP
- HTTP: Anywhere
- HTTPS: Anywhere

Việc chỉ mở SSH cho địa chỉ IP của bản thân giúp hạn chế nguy cơ bị truy cập trái phép.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog36.png)

---

## 3.9.3 Cấu hình Outbound Rule

Đối với Outbound Rule, tôi giữ nguyên cấu hình mặc định.

Điều này cho phép EC2 chủ động kết nối ra Internet để:

- Cập nhật hệ điều hành.
- Tải package.
- Gọi API.
- Kết nối các dịch vụ AWS.

Qua nội dung này, tôi hiểu rằng Security Group là lớp bảo vệ đầu tiên của mỗi tài nguyên trên AWS và nên tuân thủ nguyên tắc **Least Privilege**, chỉ mở các cổng thực sự cần thiết.

---

## 3.10 Tìm hiểu Network ACL

Sau khi tìm hiểu Security Group, tôi tiếp tục nghiên cứu **Network Access Control List (Network ACL hay NACL)**.

Network ACL là một lớp tường lửa hoạt động ở **cấp Subnet**, dùng để kiểm soát lưu lượng mạng đi vào (Inbound) và đi ra (Outbound) của toàn bộ Subnet.

Khác với Security Group chỉ áp dụng cho từng EC2 hoặc từng tài nguyên, Network ACL sẽ áp dụng cho tất cả các tài nguyên nằm trong cùng một Subnet.

---

### 3.10.1 Tìm hiểu các thành phần của Network ACL

Trong quá trình học, tôi tìm hiểu các thành phần chính của Network ACL.

| Thành phần | Chức năng |
|------------|-----------|
| Rule Number | Thứ tự ưu tiên của luật |
| Type | Loại giao thức hoặc dịch vụ |
| Protocol | Giao thức mạng |
| Port Range | Phạm vi cổng |
| Source/Destination | Địa chỉ IP nguồn hoặc đích |
| Allow | Cho phép lưu lượng |
| Deny | Từ chối lưu lượng |

AWS sẽ đọc các Rule theo thứ tự từ nhỏ đến lớn và áp dụng luật đầu tiên phù hợp.

---

### 3.10.2 So sánh Security Group và Network ACL

Sau khi nghiên cứu cả hai cơ chế bảo mật, tôi tổng hợp sự khác nhau như sau:

| Tiêu chí | Security Group | Network ACL |
|----------|----------------|-------------|
| Áp dụng | EC2, RDS, Lambda... | Subnet |
| Hoạt động | Stateful | Stateless |
| Có Rule Deny | Không | Có |
| Mặc định | Từ chối toàn bộ Inbound | Cho phép toàn bộ |
| Quản lý | Đơn giản | Chi tiết hơn |

Qua quá trình tìm hiểu, tôi nhận thấy:

- **Security Group** phù hợp để kiểm soát quyền truy cập của từng tài nguyên.
- **Network ACL** phù hợp để kiểm soát lưu lượng của toàn bộ Subnet.

Hai cơ chế này thường được sử dụng kết hợp nhằm tăng cường khả năng bảo mật cho hệ thống.

---

### 3.10.3 Nguyên tắc nhiều lớp bảo mật

Trong quá trình học, tôi hiểu được AWS áp dụng mô hình **Defense in Depth** (bảo mật nhiều lớp).

Một yêu cầu từ Internet đến EC2 thường sẽ phải đi qua nhiều lớp kiểm tra:

```text
Internet
     │
     ▼
Internet Gateway
     │
     ▼
Route Table
     │
     ▼
Network ACL
     │
     ▼
Security Group
     │
     ▼
EC2 Instance
```

Nếu một trong các lớp từ chối lưu lượng thì yêu cầu sẽ không thể đến được EC2.

Nhờ vậy hệ thống sẽ an toàn hơn so với chỉ sử dụng một lớp Firewall.

---

## 3.11 Thiết kế kiến trúc mạng

Sau khi hoàn thành các nội dung lý thuyết và thực hành, tôi tiến hành thiết kế mô hình mạng tổng thể cho dự án.

Mục tiêu của mô hình là:

- Phân chia tài nguyên hợp lý.
- Đảm bảo khả năng mở rộng.
- Tăng cường bảo mật.
- Phù hợp với kiến trúc triển khai trên AWS.

Kiến trúc gồm:

- 01 Amazon VPC.
- 02 Availability Zone.
- Public Subnet.
- Private Subnet.
- Internet Gateway.
- Route Table.
- Security Group.

Trong quá trình học, tôi chưa triển khai NAT Gateway do dịch vụ này phát sinh chi phí ngoài AWS Free Tier, tuy nhiên vẫn nghiên cứu cách hoạt động để phục vụ việc thiết kế kiến trúc.

---

### 3.11.1 Mô hình kiến trúc

```text
                     Internet
                         │
                         ▼
                Internet Gateway
                         │
                ┌────────┴────────┐
                │                 │
          Amazon VPC (10.0.0.0/16)
                │
      ┌─────────┴─────────┐
      │                   │
      ▼                   ▼
Public Subnet        Private Subnet
10.0.1.0/24          10.0.2.0/24
      │                   │
      ▼                   ▼
 Amazon EC2         Backend / Database
      │
Security Group
```

Đây là mô hình mạng cơ bản và được sử dụng phổ biến trong nhiều hệ thống triển khai trên AWS.

---

### 3.11.2 Luồng truy cập

Trong mô hình trên, luồng dữ liệu diễn ra như sau:

1. Người dùng gửi yêu cầu từ Internet.
2. Yêu cầu đi qua Internet Gateway.
3. Route Table xác định đường đi.
4. Security Group kiểm tra quyền truy cập.
5. EC2 tiếp nhận và xử lý yêu cầu.

Đối với các tài nguyên đặt trong Private Subnet, người dùng từ Internet sẽ không thể truy cập trực tiếp.

---

## 3.12 Khó khăn gặp phải

Trong quá trình học tập và thực hành, tôi gặp một số khó khăn như:

- Khó hình dung mối quan hệ giữa VPC, Subnet và Availability Zone.
- Chưa hiểu sự khác nhau giữa Public Subnet và Private Subnet.
- Dễ nhầm lẫn vai trò của Internet Gateway và Route Table.
- Chưa phân biệt rõ Security Group và Network ACL.
- Khó hình dung đường đi của dữ liệu giữa Internet và các tài nguyên trong VPC.

Các khái niệm này đều liên quan chặt chẽ với nhau nên nếu chỉ học lý thuyết sẽ khá khó tiếp cận.

---

## 3.13 Cách giải quyết

Để khắc phục những khó khăn trên, tôi áp dụng nhiều phương pháp học tập khác nhau.

Trước tiên, tôi sử dụng AWS Management Console để trực tiếp tạo các thành phần như VPC, Subnet, Internet Gateway và Route Table. Việc thao tác trực tiếp giúp tôi hiểu rõ chức năng của từng dịch vụ.

Bên cạnh đó, tôi xây dựng các sơ đồ kiến trúc mạng nhằm mô tả mối quan hệ giữa các thành phần và đường đi của dữ liệu.

Ngoài ra, tôi thực hiện so sánh Security Group và Network ACL thông qua bảng tổng hợp để dễ dàng ghi nhớ sự khác biệt giữa hai cơ chế bảo mật.

Sau khi kết hợp giữa lý thuyết và thực hành, tôi đã có thể hình dung rõ cách một hệ thống mạng hoạt động trên nền tảng AWS.

---

## 3.14 Kiến thức đạt được

Sau khi hoàn thành tuần thứ ba, tôi đạt được các kiến thức và kỹ năng sau:

- Hiểu vai trò của Amazon VPC trong việc xây dựng hạ tầng mạng trên AWS.
- Biết cách tạo và cấu hình Amazon VPC.
- Hiểu nguyên lý hoạt động của CIDR Block.
- Biết cách tạo Public Subnet và Private Subnet.
- Hiểu chức năng của Internet Gateway.
- Biết cách cấu hình Route Table.
- Hiểu nguyên lý hoạt động của NAT Gateway.
- Phân biệt Security Group và Network ACL.
- Hiểu nguyên tắc thiết kế mạng nhiều lớp trên AWS.
- Thiết kế được mô hình mạng cơ bản phục vụ triển khai ứng dụng.

---

## 3.15 Đánh giá của bản thân

Tuần thứ ba là một trong những tuần học quan trọng nhất trong chương trình thực tập vì giúp tôi hiểu nền tảng mạng của các dịch vụ AWS.

Ban đầu, các khái niệm như CIDR Block, Route Table, Internet Gateway hay Network ACL tương đối khó hình dung do liên quan đến kiến thức mạng máy tính. Tuy nhiên, thông qua việc thực hành trực tiếp trên AWS Console, kết hợp với việc tự xây dựng sơ đồ kiến trúc và phân tích luồng dữ liệu, tôi đã hiểu rõ hơn cách các thành phần phối hợp với nhau để tạo thành một hệ thống mạng hoàn chỉnh.

Những kiến thức đạt được trong tuần này là nền tảng quan trọng để tôi tiếp tục nghiên cứu và triển khai các dịch vụ như AWS Lambda, Amazon API Gateway, Amazon Cognito và các kiến trúc Serverless trong những tuần tiếp theo.