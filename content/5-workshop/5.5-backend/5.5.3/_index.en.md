+++
title = '5.5.3 Create an IAM Role for AWS Lambda'
weight = 3

[params]
  collapsibleMenu = true
+++

## Create an IAM Role for AWS Lambda

AWS Lambda requires permission to interact with other AWS services. Instead of embedding AWS credentials inside the application, AWS recommends assigning an IAM Role to each Lambda function.

In this project, the Lambda execution role will allow the function to:

- Generate speech using Amazon Polly.
- Upload audio files to Amazon S3.
- Read and write conversion history in Amazon DynamoDB.
- Write execution logs to Amazon CloudWatch.

Following the Principle of Least Privilege, the role should only include the permissions required for the Polly Voice application.

---

## Architecture

The relationship between AWS Lambda and the AWS services is illustrated below.

```text
AWS Lambda
      │
      ├────────► Amazon Polly
      │
      ├────────► Amazon S3
      │
      ├────────► Amazon DynamoDB
      │
      └────────► Amazon CloudWatch
```

> **Insert architecture screenshot here.**

---

## Step 1 – Open AWS Identity and Access Management (IAM)

Sign in to the **AWS Management Console**.

Search for **IAM**.

Open the **AWS Identity and Access Management (IAM)** service.

> **Insert screenshot of the IAM console.**

---

## Step 2 – Create a New Role

Navigate to:

**Access management → Roles**

Click **Create role**.

> **Insert screenshot of the Create Role page.**

---

## Step 3 – Select the Trusted Entity

Choose the following options:

| Setting | Value |
|----------|-------|
| Trusted entity type | AWS service |
| Use case | Lambda |

Click **Next**.

This configuration allows AWS Lambda to assume the role whenever a function is executed.

> **Insert screenshot of the trusted entity configuration.**

---

## Step 4 – Add Permissions

Attach the following AWS managed policies.

| Policy | Purpose |
|----------|---------|
| AWSLambdaBasicExecutionRole | Write logs to Amazon CloudWatch |
| AmazonPollyFullAccess* | Generate speech using Amazon Polly |
| AmazonS3FullAccess* | Upload audio files to Amazon S3 |
| AmazonDynamoDBFullAccess* | Read and write conversion history |

> **Insert screenshot of the permission selection page.**

> **Note:**  
> For simplicity, this workshop uses several AWS managed policies. In a production environment, these permissions should be replaced with custom IAM policies that grant access only to the required resources and actions.

---

## Step 5 – Name the Role

Configure the role information.

| Setting | Value |
|----------|-------|
| Role name | PollyVoiceLambdaRole |
| Description | IAM role for Polly Voice Lambda functions |

Click **Create role**.

> **Insert screenshot of the role review page.**

---

## Step 6 – Review the Role

Open the newly created role.

Verify that:

- The trusted entity is **AWS Lambda**.
- All required permission policies are attached.
- The role status is active.

> **Insert screenshot of the created IAM role.**

---

## IAM Best Practices

When deploying applications to production, we should follow these security best practices:

- Grant only the minimum permissions required.
- Avoid using wildcard (`*`) permissions whenever possible.
- Restrict access to specific S3 buckets and DynamoDB tables.
- Separate development and production IAM roles.
- Regularly review and audit IAM permissions.

Applying these practices reduces security risks and helps protect AWS resources from unauthorized access.

---

## Expected Result

After completing this section, we have successfully created an IAM execution role for AWS Lambda.

The role is now able to:

- Generate speech using Amazon Polly.
- Upload generated audio files to Amazon S3.
- Store and retrieve metadata from Amazon DynamoDB.
- Write execution logs to Amazon CloudWatch.

This IAM role will be attached to the Lambda functions in the next section of the workshop.