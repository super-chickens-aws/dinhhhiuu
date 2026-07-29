+++
title = "1.3 Week 3 - Exploring Amazon VPC and Networking"
weight = 3

[params]
  collapsibleMenu = true
+++

## Objectives

During the third week, I focused on studying the network architecture on Amazon Web Services (AWS). This was one of the most important topics because most AWS services operate within a private network managed by Amazon Virtual Private Cloud (Amazon VPC).

The objectives of this week were:

- Understand the AWS network architecture.
- Learn how to build an Amazon VPC.
- Understand how to divide a network using Subnets.
- Learn how Internet connectivity works for a VPC.
- Understand the security components of the AWS networking system.
- Design a network architecture for application deployment.

---

## 3.1 Understanding Amazon VPC

Amazon Virtual Private Cloud (Amazon VPC) is a service that allows users to create a private network (Virtual Network) on AWS for deploying resources such as Amazon EC2, Amazon RDS, and AWS Lambda.

A VPC can be considered similar to an organization's internal network, where users have full control over:

- The IP address range.
- How the network is divided into multiple Subnets.
- Which resources are allowed to access the Internet.
- The communication flow between resources within the system.

As a result, the entire infrastructure is isolated from other AWS customers and can be configured according to the specific requirements of each application.

During this study, I learned about the main components of Amazon VPC.

| Component | Function |
|------------|-----------|
| VPC | A private network that contains all resources of the system |
| Subnet | Divides the VPC into multiple smaller networks |
| Route Table | Routes network traffic |
| Internet Gateway | Allows the VPC to connect to the Internet |
| NAT Gateway | Allows Private Subnets to access the Internet |
| Security Group | Firewall at the resource level |
| Network ACL | Firewall at the Subnet level |

Through this study, I understood that Amazon VPC is the foundation of most services deployed on AWS.

![Image description](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog26.webp)

---

## 3.2 Creating an Amazon VPC

After learning the theoretical concepts, I created an Amazon VPC for the practical exercises in this week.

Navigate to:

**AWS Management Console → Amazon VPC → Your VPCs → Create VPC**

---

### 3.2.1 Configuring the VPC

On the VPC creation page, I configured the following settings.

| Property | Value |
|------------|----------|
| Resources to create | VPC only |
| Name tag | demo-vpc |
| IPv4 CIDR | 10.0.0.0/16 |
| IPv6 CIDR | No IPv6 CIDR Block |
| Tenancy | Default |

Where:

- **Name tag** helps identify the VPC during management.
- **IPv4 CIDR** defines the IP address range of the entire network.
- **Tenancy** is left as the default setting to use AWS shared infrastructure without additional costs.

![Image description](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog27.png)

---

### 3.2.2 Understanding CIDR Blocks

While creating the VPC, I also learned about CIDR Blocks.

CIDR (Classless Inter-Domain Routing) is a method for representing IP address ranges.

For example:

```text
10.0.0.0/16
```

Where:

- `10.0.0.0` is the network address.
- `/16` indicates the number of bits used for the network portion.

A `/16` CIDR Block provides a total of:

```text
65,536 IP addresses
```

This address range can be further divided into multiple smaller Subnets.

For example:

| Subnet | CIDR |
|---------|------|
| Public Subnet | 10.0.1.0/24 |
| Private Subnet | 10.0.2.0/24 |
| Private Subnet | 10.0.3.0/24 |

Through this study, I understood that a CIDR Block determines the size of the entire network.

---

### 3.2.3 Creating the VPC

After completing the configuration, I selected:

**Create VPC**

Within a few seconds, AWS successfully created a new VPC.

On the management page, I verified the following information:

- VPC ID
- State
- IPv4 CIDR
- Default Route Table
- Default Network ACL

Through this exercise, I observed that AWS automatically creates a default Route Table and a default Network ACL whenever a new VPC is created.

![Image description](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog28.png)

---

## 3.3 Understanding Subnets

After creating the VPC, I continued learning about Subnets.

A Subnet is a smaller network that is created within a VPC for different deployment purposes.

A VPC can contain multiple Subnets, and each Subnet belongs to only one Availability Zone.

Dividing a VPC into multiple Subnets provides several benefits:

- Easier network management.
- Improved security.
- Better scalability.
- Separation of application components.

In general, there are two types of Subnets.

| Type | Purpose |
|------|----------|
| Public Subnet | Hosts resources that require Internet access |
| Private Subnet | Hosts internal resources |

Example:

Public Subnet:

```text
10.0.1.0/24
```

Private Subnet:

```text
10.0.2.0/24
```

Through this study, I understood that separating resources into Public and Private Subnets is a common design principle in modern cloud architectures.

![Image description](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog29.webp)

---

## 3.4 Creating a Public Subnet

After creating the VPC, I proceeded to create a Public Subnet.

Navigate to:

**Amazon VPC → Subnets → Create subnet**

---

### 3.4.1 Configuring the Public Subnet

On the Subnet creation page, I configured the following settings:

| Property | Value |
|------------|----------|
| VPC ID | demo-vpc |
| Subnet name | public-subnet-1 |
| Availability Zone | ap-southeast-1a |
| IPv4 CIDR | 10.0.1.0/24 |

Where:

- **VPC ID** specifies which VPC the Subnet belongs to.
- **Availability Zone** specifies where the Subnet will be deployed.
- **CIDR Block** defines the IP address range of the Subnet.

The CIDR Block:

```text
10.0.1.0/24
```

provides approximately 256 IP addresses for the Subnet.

---

### 3.4.2 Creating the Public Subnet

After completing the configuration, I selected:

**Create subnet**

AWS successfully created the Public Subnet.

On the management page, I verified the following information:

- Subnet ID
- Availability Zone
- CIDR Block
- Available IP Address

Through this exercise, I learned that a Public Subnet can only access the Internet after it is configured with both an Internet Gateway and a Route Table.

![Image description](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog30.png)

---

## 3.5 Creating a Private Subnet

In addition to the Public Subnet, I continued by creating a Private Subnet to host internal resources.

The steps are similar to those for creating a Public Subnet.

Navigate to:

**Amazon VPC → Subnets → Create subnet**

Then configure:

| Property | Value |
|------------|----------|
| VPC ID | demo-vpc |
| Subnet name | private-subnet-1 |
| Availability Zone | ap-southeast-1a |
| IPv4 CIDR | 10.0.2.0/24 |

After completing the configuration, select:

**Create subnet**

AWS successfully creates the Private Subnet.

Unlike a Public Subnet, a Private Subnet is not directly connected to the Internet. Resources typically deployed in a Private Subnet include:

- Amazon RDS.
- Backend Servers.
- Internal Services.
- Application Servers.

Separating critical resources into a Private Subnet helps reduce the risk of unauthorized access from the Internet, thereby improving the overall security of the system.

![Image description](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog31.png)

---

## 3.6 Creating an Internet Gateway

After creating the VPC and the Subnets, I continued learning about the Internet Gateway (IGW).

An **Internet Gateway** is a component that allows resources within an Amazon VPC to communicate with the Internet. Without an Internet Gateway, EC2 instances inside the VPC cannot access the Internet or receive requests from external users.

It can be considered as the "gateway" connecting the entire VPC to the Internet.

---

### 3.6.1 Creating an Internet Gateway

Navigate to:

**Amazon VPC → Internet Gateways → Create Internet Gateway**

Then configure:

| Property | Value |
|------------|----------|
| Name tag | demo-igw |

After completing the configuration, select:

**Create Internet Gateway**

AWS successfully creates a new Internet Gateway.

![Image description](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog32.png)

---

### 3.6.2 Attaching the Internet Gateway to the VPC

After creating the Internet Gateway, it must be attached to the VPC so that the VPC can connect to the Internet.

Navigate to:

**Internet Gateway → Actions → Attach to VPC**

Select:

**VPC:** `demo-vpc`

Then choose:

**Attach Internet Gateway**

When the status changes to **Attached**, the Internet Gateway has been successfully connected to the VPC.

![Image description](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog33.png)

---

### 3.6.3 Role of the Internet Gateway

The Internet Gateway is responsible for:

- Allowing resources in the Public Subnet to access the Internet.
- Allowing users on the Internet to access resources that have a Public IP address.
- Performing Network Address Translation (NAT) between public IP addresses and private IP addresses within the VPC.

However, having an Internet Gateway alone is not enough. To allow an EC2 instance to access the Internet, a **Route Table** must also be configured.

---

## 3.7 Configuring a Route Table

After attaching the Internet Gateway to the VPC, I continued by configuring the Route Table.

A **Route Table** is a routing table used to determine the path that network traffic follows within the system.

It can be thought of as a "road map" that tells AWS where network packets should be sent.

---

### 3.7.1 Understanding the Default Route Table

When a VPC is created, AWS automatically creates a default Route Table.

This Route Table usually contains only one route:

| Destination | Target |
|-------------|--------|
| 10.0.0.0/16 | local |

This means that:

All resources within the VPC can communicate with one another.

However, Internet connectivity is still unavailable at this stage.

---

### 3.7.2 Creating a Route to the Internet

To allow the Public Subnet to access the Internet, I added a new route.

Navigate to:

**Amazon VPC → Route Tables → Select the Route Table → Edit routes**

Add the following route:

| Destination | Target |
|-------------|--------|
| 0.0.0.0/0 | Internet Gateway |

Where:

```text
Destination: 0.0.0.0/0
```

represents the entire Internet.

For the **Target**, select the Internet Gateway that was created earlier.

Then choose:

**Save Changes**

![Image description](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog34.png)

---

### 3.7.3 Associating the Route Table with the Public Subnet

After adding the route, the Route Table must be associated with the Public Subnet.

Navigate to:

**Route Table → Subnet Associations → Edit**

Select:

`public-subnet-1`

Then save the changes.

From this point onward, the Public Subnet has a valid route to the Internet.

![Image description](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog35.png)

---

### 3.7.4 Verifying the Configuration

After completing the configuration:

- EC2 instances in the Public Subnet can access the Internet.
- Software can be installed using `yum` or `dnf`.
- Packages can be downloaded from the Internet.
- SSH connections from a personal computer are allowed if permitted by the Security Group.

Through this practice, I understood that the Internet Gateway serves only as the "gateway" to the Internet, while the Route Table determines whether network traffic is allowed to pass through that gateway.

## 3.8 Understanding NAT Gateway

After the Public Subnet was working correctly, I continued learning about the NAT Gateway.

During this internship, I did not deploy a NAT Gateway because this service incurs costs outside the AWS Free Tier. However, I studied its operating principles.

A NAT Gateway allows resources inside a Private Subnet to access the Internet while preventing direct inbound connections from the Internet.

For example:

- Updating the operating system.
- Installing packages.
- Calling AWS APIs.
- Accessing the Internet to download data.

At the same time, users on the Internet cannot directly SSH into EC2 instances located in the Private Subnet.

---

### 3.8.1 Operating Principle

The data flow is as follows:

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

When an EC2 instance in the Private Subnet sends a request to the Internet:

- The request is forwarded to the NAT Gateway.
- The NAT Gateway sends the request to the Internet on behalf of the EC2 instance.
- The response returns to the NAT Gateway.
- The NAT Gateway forwards the response back to the EC2 instance.

As a result:

- The EC2 instance can access the Internet.
- The Internet cannot directly initiate connections to the EC2 instance.

---

### 3.8.2 Elastic IP

While studying the NAT Gateway, I also learned about Elastic IP.

An Elastic IP is a static public IPv4 address provided by AWS.

Elastic IP is commonly used for:

- NAT Gateway.
- Bastion Host.
- Servers that require a fixed public IP address.

Unlike a regular public IP address, an Elastic IP remains unchanged even after the EC2 instance is restarted.

---

## 3.9 Learning About Security Groups

After completing the networking section, I continued learning about Security Groups.

A Security Group acts as a firewall for individual AWS resources.

Each EC2 instance can be associated with one or more Security Groups.

A Security Group only allows the traffic explicitly defined in its rules. All other traffic is automatically denied.

---

### 3.9.1 Creating a Security Group

Go to:

**Amazon EC2 → Security Groups → Create Security Group**

Then configure the following:

| Property | Value |
|----------|-------|
| Name | web-sg |
| VPC | demo-vpc |
| Description | Security Group for the Web Server |

---

### 3.9.2 Configuring Inbound Rules

During this exercise, I configured the following ports:

| Port | Protocol | Purpose |
|------|----------|---------|
| 22 | SSH | Server administration |
| 80 | HTTP | Website |
| 443 | HTTPS | Secure website |

Source:

- SSH: My IP
- HTTP: Anywhere
- HTTPS: Anywhere

Allowing SSH access only from my own IP address helps reduce the risk of unauthorized access.

![Image Description](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog36.png)

---

### 3.9.3 Configuring Outbound Rules

For the Outbound Rules, I kept the default configuration.

This allows the EC2 instance to initiate outbound connections to:

- Update the operating system.
- Download packages.
- Call APIs.
- Connect to AWS services.

Through this exercise, I understood that the Security Group is the first layer of protection for AWS resources and should follow the **Least Privilege** principle by opening only the ports that are actually required.

---

## 3.10 Understanding Network ACL

After learning about Security Groups, I continued studying **Network Access Control Lists (Network ACLs or NACLs)**.

A Network ACL is a firewall that operates at the **Subnet level** and controls both inbound and outbound network traffic for an entire Subnet.

Unlike Security Groups, which apply to individual EC2 instances or resources, a Network ACL applies to all resources within the same Subnet.

---

### 3.10.1 Understanding the Components of a Network ACL

During this section, I learned about the main components of a Network ACL.

| Component | Function |
|-----------|----------|
| Rule Number | Rule priority |
| Type | Protocol or service type |
| Protocol | Network protocol |
| Port Range | Port range |
| Source/Destination | Source or destination IP address |
| Allow | Allow traffic |
| Deny | Deny traffic |

AWS evaluates the rules from the lowest rule number to the highest and applies the first matching rule.

---

### 3.10.2 Comparing Security Groups and Network ACLs

After studying both security mechanisms, I summarized their differences as follows:

| Criteria | Security Group | Network ACL |
|----------|----------------|-------------|
| Applies to | EC2, RDS, Lambda, etc. | Subnet |
| Behavior | Stateful | Stateless |
| Supports Deny Rules | No | Yes |
| Default Behavior | Deny all inbound traffic | Allow all traffic |
| Management | Simpler | More detailed |

Through this comparison, I concluded that:

- **Security Groups** are suitable for controlling access to individual resources.
- **Network ACLs** are suitable for controlling traffic for an entire Subnet.

These two mechanisms are commonly used together to strengthen the security of AWS systems.

### 3.10.3 The Principle of Defense in Depth

During this internship, I learned that AWS applies the **Defense in Depth** security model.

A request from the Internet to an EC2 instance typically passes through multiple security layers:

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

If any of these layers denies the traffic, the request cannot reach the EC2 instance.

As a result, the system is more secure than relying on only a single firewall layer.

---

## 3.11 Designing the Network Architecture

After completing both the theoretical study and hands-on practice, I designed an overall network architecture for the project.

The objectives of this architecture are:

- Organize resources appropriately.
- Ensure scalability.
- Improve security.
- Support deployment on AWS.

The architecture includes:

- One Amazon VPC.
- Two Availability Zones.
- Public Subnet.
- Private Subnet.
- Internet Gateway.
- Route Table.
- Security Group.

During this internship, I did not deploy a NAT Gateway because it incurs costs outside the AWS Free Tier. However, I studied how it works to support the architecture design.

---

### 3.11.1 Architecture Diagram

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

This is a basic network architecture that is commonly used when deploying systems on AWS.

---

### 3.11.2 Request Flow

In the architecture above, the request flow is as follows:

1. A user sends a request from the Internet.
2. The request passes through the Internet Gateway.
3. The Route Table determines the network path.
4. The Security Group checks the access permissions.
5. The EC2 instance receives and processes the request.

For resources located in the Private Subnet, users on the Internet cannot access them directly.

---

## 3.12 Challenges Encountered

During the learning and practice process, I encountered several challenges:

- Difficulty understanding the relationship between VPC, Subnet, and Availability Zone.
- Not clearly understanding the difference between Public Subnets and Private Subnets.
- Confusion about the roles of the Internet Gateway and the Route Table.
- Difficulty distinguishing between Security Groups and Network ACLs.
- Difficulty visualizing the data flow between the Internet and resources inside a VPC.

These concepts are closely related, making them difficult to understand by studying theory alone.

---

## 3.13 Solutions

To overcome these challenges, I applied several learning approaches.

First, I used the AWS Management Console to create components such as VPCs, Subnets, Internet Gateways, and Route Tables. Working directly with these services helped me better understand the purpose of each component.

In addition, I created network architecture diagrams to illustrate the relationships between components and the flow of network traffic.

I also compared Security Groups and Network ACLs using a summary table, making it easier to understand and remember the differences between these two security mechanisms.

By combining theoretical knowledge with hands-on practice, I was able to clearly understand how a network operates on the AWS platform.

---

## 3.14 Knowledge Gained

After completing the third week, I achieved the following knowledge and skills:

- Understand the role of Amazon VPC in building network infrastructure on AWS.
- Know how to create and configure an Amazon VPC.
- Understand how CIDR Blocks work.
- Know how to create Public and Private Subnets.
- Understand the purpose of an Internet Gateway.
- Know how to configure a Route Table.
- Understand how a NAT Gateway works.
- Distinguish between Security Groups and Network ACLs.
- Understand the principles of layered network security on AWS.
- Design a basic network architecture for application deployment.

---

## 3.15 Self-Evaluation

The third week was one of the most important weeks of the internship because it helped me understand the networking foundation of AWS services.

At first, concepts such as CIDR Blocks, Route Tables, Internet Gateways, and Network ACLs were relatively difficult to understand because they involve computer networking knowledge. However, by practicing directly in the AWS Management Console, creating my own architecture diagrams, and analyzing network traffic flows, I gradually gained a clear understanding of how these components work together to build a complete network system.

The knowledge and skills I gained during this week provide an important foundation for studying and implementing services such as AWS Lambda, Amazon API Gateway, Amazon Cognito, and Serverless architectures in the following weeks.