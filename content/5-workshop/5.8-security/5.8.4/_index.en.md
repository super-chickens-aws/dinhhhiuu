+++
title = '5.8.4 Secure AWS Resources with IAM'
weight = 4

[params]
  collapsibleMenu = true
+++

## Secure AWS Resources with IAM

To improve the overall security of the Polly Voice application, we configure IAM permissions following the **Principle of Least Privilege**. Each AWS service is granted only the permissions required to perform its specific tasks.

This approach minimizes security risks and helps prevent unauthorized access to AWS resources.

---

## Lambda Execution Role

Navigate to:

**AWS Console → IAM → Roles**

Select the execution role attached to the Polly Voice Lambda function.

Verify that the role contains only the permissions required by the application.

The Lambda function should have permissions to:

- Invoke Amazon Polly
- Upload audio files to Amazon S3
- Read and write items in Amazon DynamoDB
- Write logs to Amazon CloudWatch Logs

It should **not** have administrator-level permissions or access to unrelated AWS services.

> **Screenshot:** Lambda Execution Role in IAM.

---

## Amazon S3 Permissions

The Lambda function requires permission to upload generated MP3 files into the S3 bucket.

Typical permissions include:

- `s3:PutObject`
- `s3:GetObject`
- `s3:DeleteObject` (optional)
- `s3:ListBucket` (optional)

Permissions should be restricted to the application's bucket instead of all S3 buckets.

Example resource:

```
arn:aws:s3:::polly-voice-storage
arn:aws:s3:::polly-voice-storage/*
```

> **Screenshot:** IAM policy allowing access only to the Polly Voice S3 bucket.

---

## Amazon DynamoDB Permissions

The Lambda function stores and retrieves conversion history from DynamoDB.

Grant only the required actions, such as:

- `dynamodb:GetItem`
- `dynamodb:PutItem`
- `dynamodb:UpdateItem`
- `dynamodb:DeleteItem`
- `dynamodb:Query`
- `dynamodb:Scan`

The policy should reference only the Polly Voice table.

Example resource:

```
arn:aws:dynamodb:<region>:<account-id>:table/PollyVoiceHistory
```

> **Screenshot:** DynamoDB IAM permissions.

---

## Amazon Polly Permissions

To generate speech, the Lambda function needs permission to call Amazon Polly.

The required action is:

```
polly:SynthesizeSpeech
```

No additional Polly permissions are necessary for this project.

> **Screenshot:** IAM policy containing Amazon Polly permissions.

---

## CloudWatch Logs Permissions

CloudWatch Logs enables monitoring and troubleshooting for the backend.

The Lambda execution role should include permissions such as:

- `logs:CreateLogGroup`
- `logs:CreateLogStream`
- `logs:PutLogEvents`

These permissions allow Lambda to automatically create log groups and write execution logs.

> **Screenshot:** CloudWatch Logs permissions.

---

## Security Best Practices

To further improve security, we follow several AWS best practices throughout the project:

- Apply the Principle of Least Privilege.
- Avoid using AdministratorAccess for application roles.
- Never hard-code AWS credentials in the source code.
- Store sensitive configuration values using Amplify Environment Variables.
- Authenticate all API requests with Amazon Cognito JWT tokens.
- Restrict API Gateway access to authenticated users only.
- Enable CloudWatch Logs for monitoring and troubleshooting.
- Review IAM permissions periodically as the application evolves.

---

## Expected Result

After completing this section:

- The Lambda function can access only the AWS services required by the application.
- Sensitive resources remain protected from unauthorized access.
- The application follows AWS security best practices.
- IAM permissions are easier to maintain and audit as the project grows.