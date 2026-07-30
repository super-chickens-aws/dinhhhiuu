+++
title = '5.5.2 Create an Amazon DynamoDB Table'
weight = 2

[params]
  collapsibleMenu = true
+++

## Create an Amazon DynamoDB Table

Amazon DynamoDB is used to store the metadata of each Text-to-Speech conversion.

Instead of storing the audio files themselves, DynamoDB stores information about each generated file, allowing users to view and manage their conversion history.

Each record contains information such as the user who created the audio, the original text, the selected voice, the S3 object key, and the creation timestamp.

---

## Architecture

The metadata storage workflow is illustrated below.

```text
React Application
        │
        ▼
Amazon API Gateway
        │
        ▼
AWS Lambda
        │
        ├────────► Amazon Polly
        │
        ├────────► Amazon S3
        │
        └────────► Amazon DynamoDB
```

> **Insert architecture screenshot here.**

---

## Step 1 – Open Amazon DynamoDB

Sign in to the **AWS Management Console**.

Search for **Amazon DynamoDB**.

Open the DynamoDB service.

> **Insert screenshot of the DynamoDB console.**

---

## Step 2 – Create a Table

From the DynamoDB dashboard, click **Create table**.

> **Insert screenshot of the Create Table page.**

---

## Step 3 – Configure the Table

Configure the table using the following settings.

| Setting | Value |
|----------|-------|
| Table name | PollyVoiceHistory |
| Partition key | userId (String) |
| Sort key | historyId (String) |

The **Partition Key** groups all conversion records belonging to the same user.

The **Sort Key** uniquely identifies each conversion history record and allows multiple records to exist for the same user.

> **Insert screenshot of the table configuration.**

---

## Step 4 – Configure Table Settings

Under **Table settings**, select:

| Setting | Value |
|----------|-------|
| Capacity mode | On-demand |
| Table class | Standard |

Using **On-demand** capacity allows DynamoDB to automatically scale according to application traffic without requiring manual capacity planning.

This pricing model is suitable for small projects and serverless applications because charges are based only on actual requests.

> **Insert screenshot of the Capacity mode configuration.**

---

## Step 5 – Create the Table

Review the configuration.

Click **Create table**.

Amazon DynamoDB will provision the table within a few moments.

> **Insert screenshot showing the table creation process.**

---

## Step 6 – Verify the Table

Open the newly created table.

Verify that:

- The table status is **Active**.
- The Partition Key is **userId**.
- The Sort Key is **historyId**.
- No items have been inserted yet.

At this stage, the table is empty because the backend has not generated any speech records.

> **Insert screenshot of the table overview page.**

---

## Example Data Structure

Each conversion history record will follow a structure similar to the example below.

| Attribute | Description |
|-----------|-------------|
| userId | Cognito User ID |
| historyId | Unique history identifier |
| text | Original input text |
| voiceId | Amazon Polly voice |
| languageCode | Selected language |
| s3Key | Audio file location in Amazon S3 |
| audioUrl | URL of the generated audio file |
| createdAt | Creation timestamp |

This metadata enables users to review previously generated speech without recreating the audio.

---

## Expected Result

After completing this section, we have successfully created an Amazon DynamoDB table for the Polly Voice application.

The table is now ready to:

- Store speech conversion history.
- Associate records with authenticated users.
- Support efficient retrieval of user-specific data.
- Scale automatically based on application demand.
- Serve as the metadata storage layer of the serverless architecture.