+++
title = '5.8.3 IAM Least Privilege'
weight = 8

[params]
  collapsibleMenu = true
+++

## IAM Least Privilege

A fundamental AWS security principle is the **Principle of Least Privilege (PoLP)**, which states that every user, service, or application should be granted only the permissions required to perform its intended tasks.

In the Polly Voice application, IAM Roles are used instead of long-term AWS Access Keys. Each AWS service receives only the permissions necessary for its specific responsibilities.

---

## Why Least Privilege?

Granting excessive permissions increases the risk of:

- Unauthorized access to AWS resources.
- Accidental modification or deletion of data.
- Security vulnerabilities caused by compromised credentials.
- Increased impact if a service is exploited.

Applying Least Privilege minimizes these risks while maintaining normal application functionality.

---

## IAM Roles Used in Polly Voice

The application uses several AWS managed services, each with its own responsibility.

The primary IAM Role is the **Lambda Execution Role**, which allows the backend function to interact with other AWS services.

The Lambda function requires permissions to:

- Generate speech using Amazon Polly.
- Upload audio files to Amazon S3.
- Store conversion history in Amazon DynamoDB.
- Write execution logs to Amazon CloudWatch Logs.

> 📷 **Screenshot:** Lambda Execution Role

---

## Required Permissions

The following AWS services are accessed by the Lambda function.

| AWS Service | Required Permission |
|--------------|---------------------|
| Amazon Polly | Generate speech |
| Amazon S3 | Upload audio files |
| Amazon DynamoDB | Read and write conversion records |
| Amazon CloudWatch Logs | Create log groups and write logs |

Only these permissions should be granted.

> 📷 **Screenshot:** IAM Permissions

---

## Avoid Using AdministratorAccess

During development, it may be tempting to attach the **AdministratorAccess** policy because it provides unrestricted access to all AWS services.

However, this approach should be avoided.

Instead, create a dedicated IAM Role containing only the permissions required by the Polly Voice application.

This improves security and follows AWS best practices.

---

## Protect AWS Credentials

The Polly Voice application does not store AWS Access Keys or Secret Access Keys inside the source code.

Instead:

- AWS Lambda automatically assumes its IAM Role.
- React frontend never communicates directly with AWS services using AWS credentials.
- Authentication is handled by Amazon Cognito.
- API requests are secured through JWT authorization.

This approach eliminates the risk of exposing sensitive credentials.

> 📷 **Screenshot:** Lambda Execution Role Permissions

---

## Security Benefits

Applying the Principle of Least Privilege provides several advantages:

- Reduces the attack surface.
- Protects AWS resources from unauthorized access.
- Prevents accidental resource modifications.
- Improves compliance with AWS security best practices.
- Simplifies permission management and auditing.

---

## Expected Result

After applying IAM Least Privilege:

- AWS Lambda can access only the services required by the application.
- No long-term AWS credentials are stored in the frontend or backend.
- Unauthorized actions are denied automatically.
- The Polly Voice application follows AWS security best practices while maintaining secure access to AWS resources.