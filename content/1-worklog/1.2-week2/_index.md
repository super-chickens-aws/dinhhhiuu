+++
title = "1.2 Week 2 - Introduction to Amazon EC2 and Amazon S3"
weight = 2

[params]
  collapsibleMenu = true
+++

## Objectives

During the second week, I learned about two core Amazon Web Services (AWS) services: Amazon EC2 and Amazon S3. The objective of this week was to understand how to deploy servers on the cloud, manage computing resources, store data, and become familiar with basic security mechanisms when deploying systems.

---

## 1. Learn About Amazon EC2

Amazon Elastic Compute Cloud (Amazon EC2) is a service that provides virtual servers on the Amazon Web Services (AWS) platform. It allows users to quickly launch, configure, and manage servers for application deployment without investing in physical hardware infrastructure.

Compared to traditional servers, Amazon EC2 offers advantages such as flexible scalability, rapid deployment, and a pay-as-you-go pricing model.

During this learning process, I studied the main components of Amazon EC2 as follows:

| Component | Description |
|------------|-------------|
| **Instance** | A virtual server created on AWS. Each Instance has its own operating system, CPU, RAM, storage, and IP address for running applications. |
| **Instance Type** | Defines the hardware configuration of an Instance, including the number of CPUs, memory size, network bandwidth, and intended use (General Purpose, Compute Optimized, Memory Optimized, etc.). |
| **Amazon Machine Image (AMI)** | A preconfigured operating system image that includes the operating system and required software. When creating an Instance, users select an AMI as the foundation for the server. |
| **Key Pair** | A pair of public and private keys used for authentication when connecting to an EC2 Instance. The private key is stored on the user's computer and is used to log in via SSH or Remote Desktop. |
| **Security Group** | Acts as a virtual firewall that allows users to configure inbound and outbound access rules based on IP addresses, protocols, and ports. |
| **Elastic IP** | A static IPv4 address that can be assigned to an EC2 Instance. An Elastic IP ensures that the server's IP address remains unchanged even after restarting or replacing the Instance. |

By studying these components, I understood the process of deploying a server on AWS, from selecting an operating system and hardware configuration to configuring security, connecting to, and managing the server.

### Relationship Between the Components

The process of launching an EC2 Instance can be illustrated as follows:

![Image description](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog13.png)

The diagram above shows that creating an EC2 Instance requires selecting an AMI and an Instance Type first. After that, a Key Pair is configured for server login, a Security Group is configured to control access, and an Elastic IP can be assigned if a static IP address is required.

---

## 2. Launch an Amazon EC2 Instance

After learning the basic concepts of Amazon EC2, I proceeded to launch my first virtual server on AWS.

Sign in to the **AWS Management Console**, then navigate to:

**Amazon EC2 → Instances → Launch instances**

On the **Launch an instance** page, configure the following settings.

---

### 2.1 Name the EC2 Instance

Under **Name and tags**, enter a name for the server.

Example:

```text
tts-server
```

Assigning a meaningful name makes it easier to identify and manage the EC2 Instance during development.

---

### 2.2 Select an Amazon Machine Image (AMI)

Under **Application and OS Images (Amazon Machine Image)**, select:

```text
Amazon Linux 2023 AMI
```

Amazon Linux is an operating system developed and optimized by AWS for AWS services. It is regularly updated with performance improvements and security patches.

![Image description](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog14.png)

---

### 2.3 Select an Instance Type

Under **Instance type**, choose:

```text
t2.micro
```

This configuration is included in the **AWS Free Tier** and is suitable for learning and deploying small applications.

Basic specifications:

- 1 vCPU
- 1 GB RAM

---

### 2.4 Create a Key Pair

Under **Key pair (login)**, select:

**Create new key pair**

Then configure the following settings:

| Property | Value |
|----------|-------|
| Key pair name | `tts-key` |
| Key pair type | RSA |
| Private key file format | `.pem` |

Click **Create key pair**.

The browser will automatically download the following file:

```text
tts-key.pem
```

This key is used to authenticate when connecting to the EC2 Instance via SSH.

> **Note:** The `.pem` file can only be downloaded once. If it is lost, a new Key Pair must be created.

![Image description](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog15.png)

---

### 2.5 Configure Network Settings

In the **Network settings** section, click **Edit** to modify the configuration.

Configure the following settings:

- Auto-assign Public IP: **Enable**
- Firewall (security groups): **Create security group**

Configure the following access rules:

| Type | Port | Source | Purpose |
|------|------|--------|----------|
| SSH | 22 | My IP | Allow SSH access from my computer |
| HTTP | 80 | Anywhere | Allow web traffic |
| HTTPS | 443 | Anywhere | Allow secure web traffic |

For learning purposes, the **SSH** port is only opened to my current IP address to improve security.

![Image description](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog16.png)

![Image description](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog17.png)

---

### 2.6 Launch the EC2 Instance

After completing the configuration, click:

**Launch Instance**

AWS will begin creating the EC2 Instance.

After a few seconds, the Instance status changes to:

```text
Running
```

This indicates that the server has been successfully created.

![Image description](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog18.png)

---

## 3. Connect to EC2 Using Windows Terminal

After the EC2 Instance was running, I connected to the server using the **SSH (Secure Shell)** protocol through **Windows Terminal**.

---

### 3.1 Prepare the Connection Information

First, navigate to:

**Amazon EC2 → Instances**

Select the EC2 Instance that was created. Under the **Details** section, note the following information:

- Public IPv4 Address
- Public IPv4 DNS (if needed)

Example:

```text
13.212.xxx.xxx
```

Also prepare the following file:

```text
tts-key.pem
```

which was downloaded when creating the Key Pair.

![Image description](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog19.png)

---

### 3.2 Open Windows Terminal

Open **Windows Terminal** or **PowerShell**.

Navigate to the folder containing the `.pem` file.

For example, if the file is located in the **Downloads** folder:

```powershell
cd $HOME\Downloads
```

Verify that the file exists:

```powershell
dir
```

The output should display:

```text
tts-key.pem
```

![Image description](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog20.png)

---

### 3.3 Connect to the EC2 Instance

Run the following command:

```bash
ssh -i tts-key.pem ec2-user@13.212.xxx.xxx
```

Where:

- `-i` specifies the Key Pair file.
- `tts-key.pem` is the private key file provided by AWS.
- `ec2-user` is the default user account for Amazon Linux.
- `13.212.xxx.xxx` is the Public IPv4 address of the EC2 Instance.

The first time you connect, the Terminal will display the following message:

```text
The authenticity of host '13.212.xxx.xxx' can't be established.
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

Type:

```text
yes
```

and press **Enter**.

{{% notice style="warning" title="Note for Windows Users" icon="triangle-exclamation" %}}

If you are using **Windows Terminal** and receive the following message:

```text
Permissions for 'tts-key.pem' are too open.
This private key will be ignored.
```

This means the **`.pem`** file has overly permissive access permissions. Before connecting via SSH, you need to restrict access to the private key file.

Follow these steps:

1. Right-click **`tts-key.pem`** → **Properties**.
2. Open the **Security** tab → **Advanced**.
3. Click **Disable inheritance**.
4. Select **Convert inherited permissions into explicit permissions**.
5. Remove the permissions for the **Users** group, leaving only your current Windows account (and **SYSTEM** and **Administrators**, if necessary).
6. Click **Apply** and **OK** to save the changes.

After completing these steps, run the SSH command again.

{{% /notice %}}

If the connection is successful, the Amazon Linux terminal interface will appear.

![Image description](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog21.png)

---

### 3.4 Verify the EC2 Instance

After successfully logging in, I executed several commands to verify the server status.

Check the current user:

```bash
whoami
```

Check the operating system:

```bash
cat /etc/os-release
```

Check the hostname:

```bash
hostname
```

Check disk usage:

```bash
df -h
```

Check memory usage:

```bash
free -h
```

Check the IP address:

```bash
hostname -I
```

Using these commands, I confirmed that the EC2 Instance was operating correctly and was ready for software installation or application deployment.

![Image description](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog22.png)

---

### 3.5 Result

After completing the above steps, I successfully created an Amazon EC2 Instance and connected to the server using Windows Terminal via SSH. I also became familiar with basic Linux administration tasks such as checking the operating system, disk usage, memory usage, and IP address. This provided a solid foundation for deploying applications in a cloud environment in the following sections.

---

## 4. Managing EC2 Instances

Next, I practiced managing the lifecycle of an EC2 Instance.

The operations included:

- Start Instance
- Stop Instance
- Reboot Instance
- Terminate Instance

Through these exercises, I understood the differences between stopping, restarting, and permanently deleting an EC2 Instance.

---

## 5. Learn About Amazon S3

After completing the EC2 section, I continued by learning about Amazon Simple Storage Service (Amazon S3).

Amazon S3 is AWS's object storage service.

Data is stored in the form of:

- Buckets
- Objects

Amazon S3 provides virtually unlimited storage capacity with high data durability and is widely used for storing images, videos, documents, and static files.

---

## 6. Create an Amazon S3 Bucket

After learning about Amazon S3, I created my first Bucket to store data on the AWS platform.

Sign in to the **AWS Management Console**, then navigate to:

**Amazon S3 → Buckets → Create bucket**

---

### 6.1 Specify the Bucket Name

Under **Bucket name**, enter a name for the Bucket.

Example:

```text
tts-storage-demo
```

The Bucket name must meet the following requirements:

- Contain only lowercase letters (`a-z`), numbers (`0-9`), and hyphens (`-`).
- Not contain spaces or special characters.
- Be globally unique across all Amazon S3 Buckets.

---

### 6.2 Configure Block Public Access

By default, Amazon S3 blocks all public access to help protect stored data.

During this exercise, I kept the default setting:

```text
Block all public access
```

This ensures that the Bucket can only be accessed by authorized users or AWS services with the appropriate permissions.

![Image description](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog23.png)

---

### 6.3 Create the Bucket

After completing the configuration, click:

**Create bucket**

The new Bucket will appear in the Bucket list and is ready to store data.

![Image description](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog24.png)

---

## 6.4 Upload Data to Amazon S3

After creating the Bucket, I uploaded several files to Amazon S3 to understand how data is stored using the Object Storage model.

First, open the newly created Bucket, then select:

**Upload → Add files**

Choose several files to upload, including:

- Images (`.png`, `.jpg`)
- Documents (`.pdf`)
- Static web pages (`.html`)

After selecting the files, click:

**Upload**

Amazon S3 stores each uploaded file as an **Object**.

![Image description](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog25.png)

---

### 6.5 View Uploaded Objects

After the upload is complete, each file appears in the Bucket with information such as:

| Property | Description |
|----------|-------------|
| Object Key | The unique identifier of the Object within the Bucket |
| Size | File size |
| Last Modified | The upload date and time |
| Storage Class | The storage class assigned to the Object |

Through this exercise, I learned that Amazon S3 does not organize data using traditional folders like an operating system. Instead, each file is stored as an **Object** and identified by its **Object Key**.

---

### 6.6 Learn About Storage Classes

Amazon S3 provides multiple storage classes to optimize cost and performance for different access patterns.

During this exercise, I used the default storage class:

```text
S3 Standard
```

This storage class is suitable for data that is accessed frequently.

I also explored several other storage classes:

| Storage Class | Purpose |
|---------------|---------|
| S3 Standard | Frequently accessed data |
| S3 Intelligent-Tiering | Automatically optimizes storage costs |
| S3 Standard-IA | Infrequently accessed data |
| S3 Glacier Instant Retrieval | Long-term storage with fast retrieval |
| S3 Glacier Flexible Retrieval | Backup and long-term archival |
| S3 Glacier Deep Archive | Very long-term archival with the lowest storage cost |

---

## 7. Manage Amazon S3 Access Permissions

After learning how to store data, I continued by studying Amazon S3 access control mechanisms to better understand how data security is managed.

Amazon S3 provides several methods for controlling access, including:

- Block Public Access
- Bucket Policy
- IAM Policy
- Object ACL

---

### 7.1 Block Public Access

This is the first layer of protection provided by Amazon S3.

By default, AWS enables:

```text
Block all public access
```

This prevents Buckets and Objects from being publicly accessible over the Internet.

During this exercise, I kept the default configuration to ensure that the stored data remained secure.

---

### 7.2 Bucket Policy

A Bucket Policy is a JSON-based policy that defines who can access a Bucket and what actions they are allowed to perform.

Examples include:

- Allowing users to read objects.
- Allowing users to upload files.
- Granting access only to a specific IAM User or IAM Role.

With a Bucket Policy, permissions can be managed for the entire Bucket without configuring each Object individually.

---

### 7.3 Object Permissions

In addition to Bucket Policies, individual Objects can also have their own access permissions.

During this exercise, I examined the following Object properties:

- Owner
- Permissions
- Metadata

Through this practice, I learned that an individual Object can have different access permissions from the Bucket if configured separately.

---

### 7.4 Result

After completing these exercises, I successfully created an Amazon S3 Bucket, uploaded data to the cloud, and explored Amazon S3 access control mechanisms. I also understood the roles of **Block Public Access**, **Bucket Policy**, and **Object Permissions** in protecting data on the AWS platform.

---

## 8. Challenges Encountered

During the hands-on exercises, I encountered some difficulties configuring Security Groups and connecting to the EC2 Instance via SSH because I did not fully understand network port rules and access permissions.

In addition, distinguishing the access control mechanisms between Bucket Policies and Block Public Access in Amazon S3 was initially confusing.

---

## 9. Solutions

To overcome these challenges, I referred to the official AWS documentation, reviewed the network configuration carefully, and repeatedly practiced creating EC2 Instances and S3 Buckets.

By experimenting with different configurations and comparing the results, I gained a better understanding of the security mechanisms used by Amazon EC2 and Amazon S3.

---

## 10. Knowledge Gained

After the second week, I was able to:

- Understand how Amazon EC2 works.
- Create and manage EC2 Instances.
- Configure Security Groups.
- Connect to Linux servers using SSH.
- Understand the storage model of Amazon S3.
- Create and manage S3 Buckets.
- Upload and manage Objects.
- Understand Amazon S3 security and access control mechanisms.

---

## 11. Self-Evaluation

The second week gave me hands-on experience with AWS infrastructure services by deploying EC2 Instances and storing data in Amazon S3. Creating, configuring, and managing these resources helped me better understand the process of deploying systems in a cloud environment.

The knowledge and practical skills I gained this week provide an important foundation for studying networking, system architecture, and Serverless services in the following weeks.