+++
title = '5.7.2 Test Text-to-Speech API'
weight = 2

[params]
  collapsibleMenu = true
+++

## Test Text-to-Speech API

After verifying user authentication, we should test whether the Text-to-Speech API functions correctly.

This test ensures that the frontend can successfully communicate with Amazon API Gateway, which invokes AWS Lambda to generate speech using Amazon Polly.

---

## Test Scenario

Verify the following workflow:

- Submit a valid text input.
- Generate speech using Amazon Polly.
- Receive a successful response from the backend.
- Display the generated audio on the frontend.

---

## Step 1. Enter Sample Text

After logging into the application:

1. Navigate to the **Text-to-Speech** page.
2. Enter a sample text, for example:

```text
Hello! Welcome to Polly Voice.
This application demonstrates Amazon Polly running on AWS Serverless.
```

3. Select one of the available voices.

> 📷 **Screenshot:** Enter Text and Select Voice

---

## Step 2. Generate Speech

Click the **Generate** button.

The frontend sends an HTTPS request to **Amazon API Gateway**.

API Gateway forwards the request to **AWS Lambda**, which calls **Amazon Polly** to synthesize the speech.

> 📷 **Screenshot:** Click Generate Button

---

## Step 3. Verify API Response

If the request is successful, the backend should return a response similar to:

```json
{
  "message": "Speech generated successfully.",
  "audioUrl": "https://<bucket-name>.s3.amazonaws.com/audio/example.mp3"
}
```

Verify that the response contains a valid audio URL.

> 📷 **Screenshot:** Successful API Response

---

## Step 4. Verify Audio Playback

After receiving the response:

- The audio player should appear automatically.
- Click **Play** to verify that the generated speech is correct.
- Verify that the **Download** button is available.

> 📷 **Screenshot:** Audio Player

---

## Step 5. Verify CloudWatch Logs

To confirm that the backend processed the request successfully:

1. Open the **AWS Management Console**.
2. Navigate to **CloudWatch**.
3. Select **Log groups**.
4. Open the log group for **PollyVoiceFunction**.
5. Review the latest log stream.

Verify that:

- The Lambda function was invoked successfully.
- No runtime errors occurred.
- Amazon Polly generated the speech successfully.

> 📷 **Screenshot:** Lambda Logs in CloudWatch

---

## Expected Result

The Text-to-Speech API is considered successful if:

- The frontend can send requests to API Gateway.
- API Gateway successfully invokes AWS Lambda.
- Lambda generates speech using Amazon Polly.
- A valid audio URL is returned.
- The generated audio can be played and downloaded.
- CloudWatch Logs show successful execution without errors.

This confirms that the backend API and Amazon Polly integration are functioning correctly.