+++
title = '5.8.5 IAM Least Privilege'
weight = 5

[params]
  collapsibleMenu = true
+++

## IAM Least Privilege

One of the most important security principles in AWS is the **Principle of Least Privilege**, which means every user, role, or service should receive only the permissions required to perform its intended tasks—and nothing more.

In Polly Voice, we configure IAM roles so that each AWS service has only the minimum permissions necessary. This helps reduce the attack surface, protects sensitive resources, and limits the impact of potential security incidents.

---

## Architecture

The application uses separate IAM roles for different AWS services.

- AWS Lambda executes the backend logic.
- Amazon Cognito manages user authentication.
- AWS Amplify deploys the frontend.
- API Gateway invokes Lambda.
- Amazon Polly synthesizes speech.
- Amazon S3 stores generated audio files.
- Amazon DynamoDB stores conversion history.

Each component accesses only the AWS resources required for its functionality.

> **Insert architecture diagram highlighting IAM roles here.**

---

## Lambda Execution Role

The Lambda execution role should include permissions only for the AWS services used by the application.

Required permissions include:

- Amazon Polly
  - `polly:SynthesizeSpeech`

- Amazon S3
  - `s3:GetObject`
  - `s3:PutObject`

- Amazon DynamoDB
  - `dynamodb:GetItem`
  - `dynamodb:PutItem`
  - `dynamodb:Query`

- CloudWatch Logs
  - `logs:CreateLogGroup`
  - `logs:CreateLogStream`
  - `logs:PutLogEvents`

No additional administrative permissions should be granted.

---

## API Gateway Permissions

API Gateway should only have permission to invoke the backend Lambda function.

No direct access to:

- Amazon S3
- Amazon DynamoDB
- Amazon Polly

should be granted.

This ensures that all business logic is processed through Lambda.

---

## Cognito Permissions

Amazon Cognito manages:

- User registration
- User authentication
- JWT token generation

The frontend communicates directly with Cognito.

User credentials are never processed or stored by Lambda.

---

## S3 Bucket Permissions

The S3 bucket should remain private.

Recommended configuration:

- Disable public access.
- Allow access only from the Lambda execution role.
- Do not expose generated MP3 files publicly unless temporary pre-signed URLs are used.

This protects user-generated audio from unauthorized access.

> **Insert screenshot of the S3 Bucket Permissions page here.**

---

## DynamoDB Permissions

The Lambda execution role should have access only to the required DynamoDB table.

Recommended actions include:

- Read conversion history.
- Insert new conversion records.
- Query records by user.

Avoid granting permissions to delete or modify unrelated tables.

---

## Verification

After configuring IAM permissions:

1. Open **IAM Console**.
2. Review the Lambda execution role.
3. Verify that only the required policies are attached.
4. Confirm that no AdministratorAccess policy is assigned.
5. Test the application to ensure all features continue to work correctly.

> **Insert screenshot of the IAM Role Permissions page here.**

---

## Result

At the end of this section, we have successfully implemented the Principle of Least Privilege for the Polly Voice application.

Each AWS service is granted only the permissions necessary to perform its specific responsibilities, improving the overall security of the serverless architecture while following AWS security best practices.