+++
title = '5.2 Prerequisites'
weight = 2

[params]
  collapsibleMenu = true
+++

## Prerequisites

Before starting this workshop, we need to prepare an AWS environment and several development tools. The following requirements ensure that we can complete all deployment and testing steps successfully.

---

## AWS Account

We need an active AWS account with sufficient permissions to create and manage cloud resources.

The workshop uses the following AWS services:

- AWS Amplify
- Amazon Cognito
- Amazon API Gateway
- AWS Lambda
- Amazon Polly
- Amazon S3
- Amazon DynamoDB
- AWS Identity and Access Management (IAM)
- Amazon CloudWatch

---

## AWS Region

Throughout this workshop, we use the following AWS Region:

```text
ap-southeast-1 (Singapore)
```

Using the same Region for all services simplifies the deployment process and minimizes service compatibility issues.

---

## Required IAM Permissions

The AWS account should have permission to create and manage the following resources:

- IAM Roles
- Amazon Cognito User Pools
- AWS Lambda Functions
- Amazon API Gateway
- Amazon S3 Buckets
- Amazon DynamoDB Tables
- AWS Amplify Applications
- Amazon Polly
- Amazon CloudWatch Logs

To improve security, we should follow the Principle of Least Privilege by granting only the permissions required for this workshop.

---

## Development Environment

The following software should be installed before beginning the implementation.

### Node.js

Install Node.js (LTS version) together with npm.

The frontend application is developed using React and Vite.

---

### Visual Studio Code

Visual Studio Code is recommended as the primary code editor.

Useful extensions include:

- ESLint
- Prettier
- AWS Toolkit

---

### Git

Git is used for version control and source code management.

We also recommend creating a GitHub repository for project backup and future deployment.

---

## Project Structure

The project is divided into two major components:

```text
Polly Voice
│
├── frontend
│   ├── React
│   ├── TypeScript
│   └── Vite
│
└── backend
    ├── AWS Lambda
    ├── Amazon Polly
    ├── Amazon S3
    ├── Amazon DynamoDB
    └── API Gateway
```

This separation makes the application easier to develop, deploy, and maintain.

---

## Architecture Overview

The completed application will follow the workflow below:

```text
User
   │
   ▼
AWS Amplify
   │
   ▼
Amazon Cognito
   │
   ▼
API Gateway
   │
   ▼
AWS Lambda
   │
   ├────────► Amazon Polly
   │              │
   │              ▼
   │         Speech Audio
   │
   ├────────► Amazon S3
   │
   └────────► Amazon DynamoDB
```

Authentication is handled by Amazon Cognito before requests are forwarded to API Gateway. Lambda processes each request, generates speech through Amazon Polly, stores the audio file in Amazon S3, records metadata in Amazon DynamoDB, and finally returns the result to the frontend.

---

## Before We Begin

Before proceeding to the next section, make sure that:

- We have an active AWS account.
- All required AWS services are available in the selected Region.
- Node.js and Visual Studio Code are installed.
- The project source code is ready.
- We understand the overall architecture of the application.

Once these prerequisites are completed, we can begin designing the solution architecture in the next section.