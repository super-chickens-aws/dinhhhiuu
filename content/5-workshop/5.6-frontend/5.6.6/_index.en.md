+++
title = '5.6.6 Verify Deployment'
weight = 6

[params]
  collapsibleMenu = true
+++

## Verify Deployment

After completing the frontend implementation, we need to verify that the entire Polly Voice application works correctly when deployed on AWS Amplify.

This validation ensures that all AWS services are integrated properly and that the complete Text-to-Speech workflow functions as expected.

---

## Step 1. Open the Amplify Application

1. Open the **AWS Management Console**.
2. Navigate to **AWS Amplify**.
3. Select the **Polly Voice** application.
4. Open the generated application URL.

The homepage of Polly Voice should be displayed.

> 📷 **Screenshot:** Polly Voice Homepage on AWS Amplify

---

## Step 2. Test User Authentication

Verify that Amazon Cognito authentication is working correctly.

Perform the following actions:

- Create a new account (if needed).
- Sign in using a valid account.
- Confirm that the application redirects to the main dashboard after successful authentication.

> 📷 **Screenshot:** Successful Login

---

## Step 3. Test Text-to-Speech Generation

On the dashboard:

1. Enter a sample text.
2. Select a voice.
3. Click **Generate**.

Wait for the application to process the request.

The frontend should send the request to API Gateway, which invokes the Lambda function to generate speech using Amazon Polly.

> 📷 **Screenshot:** Generate Speech Request

---

## Step 4. Verify the Generated Audio

After the request is completed, verify that:

- The audio player appears.
- The generated speech can be played successfully.
- The generated MP3 file can be downloaded.

> 📷 **Screenshot:** Audio Playback Result

---

## Step 5. Verify Stored Data

Confirm that the generated data has been stored correctly.

### Amazon S3

Open the S3 bucket and verify that:

- A new MP3 file has been created.
- The file name matches the generated request.

> 📷 **Screenshot:** Generated Audio File in Amazon S3

---

### Amazon DynamoDB

Open the DynamoDB table and verify that:

- A new record has been inserted.
- The stored information includes:
  - User ID
  - Input text
  - Selected voice
  - Audio file URL
  - Creation timestamp

> 📷 **Screenshot:** Conversion History in DynamoDB

---

## Expected Result

If all steps are completed successfully:

- Users can authenticate through Amazon Cognito.
- The frontend is accessible through AWS Amplify.
- API Gateway successfully invokes AWS Lambda.
- Amazon Polly generates speech correctly.
- Audio files are stored in Amazon S3.
- Conversion history is stored in Amazon DynamoDB.
- Users can play and download the generated audio without errors.

This confirms that the Polly Voice application has been successfully deployed and that all AWS services are working together as a complete Serverless solution.