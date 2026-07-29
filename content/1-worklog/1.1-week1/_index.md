+++
title = "1.1 Week 1 - Introduction to AWS Cloud"
weight = 1

[params]
  collapsibleMenu = true
+++

## Objectives

During the first week of the internship, I became familiar with the internship program and the Amazon Web Services (AWS) platform. The objective of this week was to understand the fundamental concepts of cloud computing, the AWS global infrastructure, user account and permission management, and to prepare the development environment for the following weeks.

---

## 1. Internship Program Overview

During the first session, I identified the following key aspects of the internship:

- Internship organization.
- Eight-week training roadmap.
- Project to be developed.
- Evaluation criteria.
- AWS services that would be used.

The learning roadmap was divided into two phases:

- **Phase 1:** Learning the core AWS services.
- **Phase 2:** Developing a Text-to-Speech application based on a Serverless architecture.

---

## 2. Understanding Cloud Computing

The first topic I studied was **Cloud Computing**.

Cloud Computing is a model that delivers computing resources over the Internet, allowing users to access servers, storage, databases, networking, and various IT services without purchasing or maintaining physical infrastructure.

During this topic, I learned about the following cloud deployment models:

- Public Cloud
- Private Cloud
- Hybrid Cloud

I also studied the three primary cloud service models:

- Infrastructure as a Service (IaaS)
- Platform as a Service (PaaS)
- Software as a Service (SaaS)

Through these concepts, I understood the advantages of Cloud Computing and why many organizations are migrating from traditional on-premises infrastructure to cloud-based solutions.

### Comparison Between On-Premises and Cloud Computing

| Criteria | On-Premises | Cloud Computing |
|-----------|-------------|-----------------|
| Infrastructure | Managed and maintained by the organization | Managed by the cloud provider |
| Initial Cost | High, requires investment in servers and hardware | Low, pay only for the resources used |
| Scalability | Limited, requires additional hardware | Easily scalable within minutes |
| Deployment Time | May take days or weeks | Can be completed within minutes |
| Maintenance | Managed by the organization | Managed by the cloud provider |
| Accessibility | Usually limited to internal networks or VPN | Accessible over the Internet with proper authorization |
| Availability | Depends on the organization's infrastructure | Designed for high availability and reliability |
| Examples | Company-owned data center | Amazon Web Services (AWS), Microsoft Azure, Google Cloud Platform |

---

## 3. Understanding AWS Global Infrastructure

After learning the fundamentals of Cloud Computing, I continued studying the global infrastructure of AWS.

The main topics included:

### Region

A **Region** is a geographical area where AWS operates one or more data centers.

Examples include:

- Singapore
- Tokyo
- Virginia

I learned how to select an appropriate Region based on user location in order to reduce latency and satisfy data residency requirements.

---

### Availability Zone

Each AWS Region consists of multiple **Availability Zones (AZs)**.

Availability Zones operate independently while remaining connected through high-speed networks.

Deploying resources across multiple Availability Zones provides several benefits:

- Improved availability.
- Higher fault tolerance.
- Reduced service interruption.

---

### Edge Location

An **Edge Location** is a network site used by AWS to deliver content closer to end users.

I learned that Edge Locations are commonly used by:

- Amazon CloudFront
- Amazon Route 53

Their primary purpose is to reduce latency and improve response times for users located in different geographical regions.

![Image Description](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog1.webp)

---

## 4. Understanding AWS Identity and Access Management (IAM)

After becoming familiar with the AWS global infrastructure, I studied **AWS Identity and Access Management (IAM)**.

IAM is an AWS service that enables administrators to securely manage users, groups, roles, and permissions for AWS resources.

Instead of sharing the root account, AWS recommends creating IAM users with appropriate permissions for each individual. This approach improves security and simplifies permission management.

The main components of IAM include:

- IAM User
- IAM Group
- IAM Role
- IAM Policy

By studying IAM, I understood how AWS implements identity and access management based on the principle of **least privilege**, where users are granted only the permissions required to perform their tasks.

---

## 4.1 Creating an IAM User

To practice IAM, I created a new IAM user.

Steps performed:

**AWS Console → IAM → Users → Create User**

Then I configured:

- User name
- AWS Management Console access

After entering the required information, I proceeded to the next step to assign permissions.

![Image Description](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog2.png)

---

## 4.2 Assigning Permissions

After creating the IAM user, I assigned permissions by adding the user to an existing IAM group.

Steps performed:

- Select **Add user to group**.
- Choose the **Administrators** group.
- Review the assigned permissions.

For learning purposes, I temporarily assigned the **AdministratorAccess** policy so that I could access all AWS services during the internship.

In a production environment, users should be granted only the minimum permissions required for their responsibilities.

![Image Description](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog3.png)

---

## 4.3 Reviewing User Information

After the IAM user was successfully created, I reviewed its information in the AWS Console.

The IAM user page provides details such as:

- User name
- ARN (Amazon Resource Name)
- Creation date
- Assigned permission groups
- Security credentials

Through this section, I became familiar with the user management interface provided by AWS and learned where to configure additional security settings when needed.

![Image Description](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog4.png)

---

## 4.4 Signing In with the IAM User

To verify that the IAM user worked correctly, I signed out of the root account and logged in using the newly created IAM user.

Steps performed:

1. Open the IAM sign-in page.
2. Enter the AWS account ID (or account alias).
3. Enter the IAM user name.
4. Enter the password.
5. Click **Sign In**.

After signing in successfully, I confirmed that the IAM user had access to the AWS Console according to the assigned permissions.

This exercise helped me understand the difference between using the root account and an IAM user for daily operations.

![Image Description](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog5.png)

---

## 4.5 Key Takeaways

After completing the IAM exercises, I gained the following knowledge:

- The purpose of AWS Identity and Access Management (IAM).
- The differences between IAM Users, Groups, Roles, and Policies.
- How to create and manage IAM users.
- How to assign permissions through IAM groups.
- Why the root account should not be used for everyday activities.
- The importance of applying the principle of least privilege when managing access to AWS resources.

The knowledge gained from this section provides a strong foundation for securely managing AWS resources throughout the remaining internship.

---

## 5. Setting Up AWS Command Line Interface (AWS CLI)

After becoming familiar with the AWS Management Console, I learned how to use the **AWS Command Line Interface (AWS CLI)**.

AWS CLI is a command-line tool provided by AWS that enables users to manage AWS services directly from a terminal without accessing the AWS Management Console.

Using AWS CLI makes it easier to automate tasks, manage cloud resources, and integrate AWS services into development workflows.

The main objectives of this section were:

- Install AWS CLI.
- Configure AWS credentials.
- Connect to an AWS account.
- Verify the connection.

---

## 5.1 Installing AWS CLI

First, I downloaded the AWS CLI installer from the official AWS website.

Official download link:

https://awscli.amazonaws.com/AWSCLIV2.msi

After downloading, I launched the installer and completed the installation by following the setup wizard.

To verify that AWS CLI was installed successfully, I opened **Windows PowerShell** and executed the following command:

```bash
aws --version
```

If the installation is successful, the terminal displays the installed version of AWS CLI.

Example:

```text
aws-cli/2.x.x Python/3.x Windows/AMD64
```

![Image Description](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog6.png)

---

## 5.2 Creating an Access Key

To allow AWS CLI to access AWS services, I created an **Access Key** for my IAM user.

Steps performed:

**AWS Console → IAM → Users → Security credentials**

Then:

- Select **Create access key**.
- Choose **Command Line Interface (CLI)** as the use case.
- Confirm the recommendation.
- Create the access key.

AWS then generated:

- Access Key ID
- Secret Access Key

These credentials are required when configuring AWS CLI.

> **Note:** The Secret Access Key is displayed only once when it is created. Therefore, it should be stored securely.

![Image Description](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog7.png)

---

## 5.3 Configuring AWS CLI

After obtaining the access keys, I configured AWS CLI by running:

```bash
aws configure
```

AWS CLI prompted me to enter the following information:

```text
AWS Access Key ID:
AWS Secret Access Key:
Default region name:
Default output format:
```

Example configuration:

```text
AWS Access Key ID: AKIAxxxxxxxxxxxxxxxx
AWS Secret Access Key: ************************
Default region name: ap-southeast-1
Default output format: json
```

After completing the configuration, AWS CLI automatically stored the credentials on the local machine.

![Image Description](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog8.png)

---

## 5.4 Verifying the Connection

To verify that AWS CLI was configured correctly, I executed the following command:

```bash
aws sts get-caller-identity
```

If the configuration is correct, AWS returns information about the current IAM user.

Example output:

```json
{
  "UserId": "AIDAXXXXXXXXXXXXXXXX",
  "Account": "123456789012",
  "Arn": "arn:aws:iam::123456789012:user/intern"
}
```

This confirmed that AWS CLI had successfully authenticated with my AWS account.

![Image Description](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog9.png)

---

## 5.5 Managing AWS Resources with AWS CLI

After successfully connecting to AWS, I experimented with several AWS CLI commands to interact with cloud resources.

Examples include:

List all S3 buckets:

```bash
aws s3 ls
```

List EC2 instances:

```bash
aws ec2 describe-instances
```

List IAM users:

```bash
aws iam list-users
```

Through these commands, I learned that AWS CLI communicates directly with AWS services using the same credentials configured earlier.

---

## 5.6 Knowledge Gained

After completing the AWS CLI practice, I gained the following knowledge:

- How to install AWS CLI on Windows.
- How to create an Access Key for an IAM user.
- How to configure AWS CLI using `aws configure`.
- How to verify authentication with `aws sts get-caller-identity`.
- How to perform basic AWS management tasks using command-line commands.

Learning AWS CLI provided a more efficient way to interact with AWS services and prepared me for automating cloud operations in the following weeks.

---

## 6. Challenges Encountered

During the first week, I encountered several challenges while learning the AWS platform.

Since this was my first experience working with cloud computing, many concepts such as Regions, Availability Zones, IAM Users, IAM Roles, IAM Policies, and Access Keys were completely new to me. At first, it was difficult to understand how these components were related and how they worked together within the AWS ecosystem.

Another challenge was distinguishing between the AWS root account and IAM users. Initially, I assumed that the root account should be used for all operations, but after studying AWS security best practices, I learned that the root account should only be used for initial account setup and a few administrative tasks.

I also experienced some difficulties while configuring AWS CLI. Incorrect Access Keys, invalid Region settings, or typing mistakes during configuration could prevent AWS CLI from connecting successfully to my AWS account.

---

## 7. Solutions

To overcome these challenges, I adopted several learning strategies.

First, I reviewed the AWS documentation and training materials provided during the internship to better understand the relationship between AWS services and their purposes.

Next, I practiced each task directly on the AWS Management Console instead of only reading the documentation. Creating IAM users, assigning permissions, generating Access Keys, and configuring AWS CLI allowed me to reinforce my understanding through hands-on experience.

Whenever I encountered configuration errors, I carefully reviewed each step, compared my settings with the documentation, and repeated the process until I obtained the expected results.

By combining theoretical knowledge with practical exercises, I gradually became more familiar with the AWS platform and gained confidence in using its core services.

---

## 8. Knowledge Gained

At the end of the first week, I had acquired the following knowledge and skills:

- Understand the fundamental concepts of Cloud Computing.
- Distinguish between Public Cloud, Private Cloud, and Hybrid Cloud.
- Understand the three primary cloud service models: IaaS, PaaS, and SaaS.
- Understand the AWS Global Infrastructure, including Regions, Availability Zones, and Edge Locations.
- Create and manage IAM users.
- Assign permissions using IAM Groups and IAM Policies.
- Understand the importance of the Principle of Least Privilege.
- Install and configure AWS CLI.
- Authenticate AWS CLI using IAM Access Keys.
- Execute basic AWS CLI commands to interact with AWS services.

These foundational concepts provide the necessary background for learning more advanced AWS services in the following weeks.

---

## 9. Self-Assessment

The first week provided me with a solid foundation in cloud computing and Amazon Web Services.

Although the concepts were new and sometimes challenging, the combination of theoretical lessons and hands-on practice helped me gradually understand how AWS services are organized and managed. In particular, working with IAM and AWS CLI gave me practical experience in managing user identities and interacting with AWS resources securely.

Overall, I successfully completed the objectives of the first week and gained the confidence needed to continue exploring more advanced AWS services such as Amazon EC2, Amazon S3, and Amazon VPC in the following weeks.