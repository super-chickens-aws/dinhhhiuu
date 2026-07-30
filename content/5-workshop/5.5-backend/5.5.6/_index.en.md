+++
title = '5.5.6 Implement Lambda Business Logic'
weight = 6

[params]
  collapsibleMenu = true
+++

## Implement Lambda Business Logic

In this section, we will complete the backend by implementing the business logic inside the Lambda function.

When an authenticated user submits text from the frontend, the Lambda function will:

1. Receive the HTTP request from Amazon API Gateway.
2. Validate the request.
3. Generate speech using Amazon Polly.
4. Upload the generated MP3 file to Amazon S3.
5. Save the conversion history in Amazon DynamoDB.
6. Return the audio URL to the frontend.

This completes the serverless backend of the Polly Voice application.

---

## Architecture

```text
React
   │
   ▼
API Gateway
   │
   ▼
AWS Lambda
   ├──────────────► Amazon Polly
   │                     │
   │              Generate MP3
   │                     ▼
   ├──────────────► Amazon S3
   │               Store Audio
   │
   ├──────────────► DynamoDB
   │              Save History
   │
   ▼
Return Audio URL
```

---

## Step 1 – Open Lambda

1. Open the AWS Management Console.
2. Navigate to **AWS Lambda**.
3. Select the function:

```text
polly-voice-backend
```

> **Screenshot:** Open Lambda Function

---

## Step 2 – Configure Environment Variables

Choose **Configuration** → **Environment variables**.

Add the following variables.

| Name | Example Value |
|------|---------------|
| BUCKET_NAME | polly-voice-audio |
| TABLE_NAME | polly-history |
| AWS_REGION | us-east-1 |

These variables allow the function to access AWS resources without hard-coding values.

> **Screenshot:** Lambda Environment Variables

---

## Step 3 – Update Lambda Code

Replace the default Lambda code with the Polly Voice backend implementation.

The function performs the following tasks:

- Parse the incoming request.
- Read the authenticated user information.
- Call Amazon Polly.
- Upload the generated MP3 file to Amazon S3.
- Save conversion history in DynamoDB.
- Return the generated audio URL.

> **Screenshot:** Lambda source code

---

## Step 4 – Deploy the Function

Choose **Deploy**.

Wait until the deployment completes successfully.

> **Screenshot:** Deploy Lambda

---

## Lambda Workflow

The business logic follows this workflow.

```text
Receive Request
        │
        ▼
Validate Input
        │
        ▼
Call Amazon Polly
        │
        ▼
Generate MP3
        │
        ▼
Upload to Amazon S3
        │
        ▼
Save Metadata
into DynamoDB
        │
        ▼
Return Audio URL
```

---

## Required IAM Permissions

The Lambda execution role must have permission to access the following services.

| AWS Service | Required Permission |
|-------------|--------------------|
| Amazon Polly | SynthesizeSpeech |
| Amazon S3 | PutObject |
| Amazon DynamoDB | PutItem |
| CloudWatch Logs | CreateLogGroup, CreateLogStream, PutLogEvents |

These permissions should follow the Principle of Least Privilege.

> **Screenshot:** Lambda Execution Role Permissions

---

## Expected Response

After a successful request, Lambda returns a JSON response similar to the following.

```json
{
    "message": "Speech generated successfully.",
    "audioUrl": "https://polly-voice-audio.s3.amazonaws.com/audio/example.mp3"
}
```

The frontend can use this URL to play or download the generated audio.

---

## Verify

Verify that the following resources have been updated successfully.

### Amazon S3

A new MP3 file has been uploaded.

> **Screenshot:** Generated MP3 in S3

---

### Amazon DynamoDB

A new record has been inserted into the history table.

Example attributes include:

- userId
- createdAt
- text
- voiceId
- audioUrl

> **Screenshot:** DynamoDB Item

---

### Amazon CloudWatch Logs

Open CloudWatch Logs and verify that:

- Lambda executed successfully.
- No runtime errors occurred.
- The execution completed without exceptions.

> **Screenshot:** CloudWatch Logs

---

## Result

We have successfully completed the backend implementation of Polly Voice.

The backend is now able to:

- Receive authenticated API requests.
- Generate speech using Amazon Polly.
- Store audio files in Amazon S3.
- Save conversion history in Amazon DynamoDB.
- Return the generated audio URL to the frontend.

The next section will build the React frontend and integrate it with the backend services.