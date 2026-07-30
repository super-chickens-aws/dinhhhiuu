+++
title = '5.6.5 Connect Backend API'
weight = 5

[params]
  collapsibleMenu = true
+++

## Connect Backend API

In this section, we will connect the React frontend to the serverless backend created in the previous chapters.

The frontend communicates with Amazon API Gateway through HTTPS requests. Every request includes the JWT Access Token issued by Amazon Cognito. API Gateway validates the token before forwarding the request to AWS Lambda.

If the authentication succeeds, Lambda generates speech using Amazon Polly, uploads the audio file to Amazon S3, stores the conversion history in Amazon DynamoDB, and returns the generated audio URL to the frontend.

---

## Request Flow

```text
User
   │
   ▼
React Frontend
   │
Generate Speech
   │
Authorization: Bearer <JWT>
   │
   ▼
Amazon API Gateway
   │
JWT Validation
   │
   ▼
AWS Lambda
   ├────────► Amazon Polly
   ├────────► Amazon S3
   └────────► Amazon DynamoDB
            │
            ▼
      Audio URL
            │
            ▼
React Frontend
```

---

## Step 1 – Configure the Backend Endpoint

Open the React project.

Configure the application to use the API Gateway endpoint that was created earlier.

The endpoint is stored in the following environment variable:

```text
VITE_API_URL
```

The frontend uses this value whenever it sends requests to the backend.

> **Screenshot:** Backend API Configuration

---

## Step 2 – Configure API Requests

The frontend sends an HTTP POST request to the backend whenever a user clicks the **Generate** button.

The request contains:

- Input text
- Selected voice
- Speech engine (if supported)
- Output format

The request is sent to:

```text
POST /tts
```

through the API Gateway endpoint.

> **Screenshot:** API Service Configuration

---

## Step 3 – Attach the Access Token

Before sending the request, the frontend retrieves the current user's Access Token from Amazon Cognito.

The token is included in the HTTP Authorization header.

Example:

```http
Authorization: Bearer <Access Token>
```

API Gateway validates this token automatically before invoking the Lambda function.

> **Screenshot:** Authorization Header

---

## Step 4 – Process the Response

If the request is successful, the backend returns a JSON response containing the generated audio URL.

Example response:

```json
{
    "message": "Speech generated successfully.",
    "audioUrl": "https://polly-voice-audio.s3.amazonaws.com/audio/example.mp3"
}
```

The frontend reads the response and updates the user interface.

> **Screenshot:** Successful API Response

---

## Step 5 – Display the Generated Audio

After receiving the audio URL, the application displays an audio player.

Users can:

- Play the generated speech.
- Pause the audio.
- Replay the audio.
- Download the generated MP3 file.

The application also updates the conversion history after the request is completed successfully.

> **Screenshot:** Audio Player

---

## Error Handling

The frontend also handles common API errors gracefully.

Examples include:

| HTTP Status | Description |
|-------------|-------------|
| 400 | Invalid input text |
| 401 | Unauthorized user |
| 403 | Permission denied |
| 500 | Internal server error |

Instead of displaying technical error messages, the application shows user-friendly notifications.

> **Screenshot:** Error Message Example

---

## Verify

Verify the complete workflow.

### Generate Speech

1. Sign in to the application.
2. Enter a text message.
3. Select a voice.
4. Choose **Generate**.

Expected result:

- The request is sent to API Gateway.
- Lambda generates speech using Amazon Polly.
- The MP3 file is uploaded to Amazon S3.
- A new record is stored in DynamoDB.
- The audio player appears on the page.

> **Screenshot:** Successful Speech Generation

---

### Verify AWS Resources

Confirm that all backend services are working correctly.

**Amazon S3**

- A new MP3 file has been uploaded.

> **Screenshot:** MP3 File in Amazon S3

---

**Amazon DynamoDB**

- A new history record has been created.

> **Screenshot:** DynamoDB Record

---

**Amazon CloudWatch**

- Lambda execution logs are generated successfully.
- No runtime errors are reported.

> **Screenshot:** CloudWatch Logs

---

## Result

We have successfully connected the React frontend to the serverless backend.

The complete request workflow now includes:

- User authentication with Amazon Cognito.
- Secure API requests through Amazon API Gateway.
- Speech synthesis using Amazon Polly.
- Audio storage in Amazon S3.
- History storage in Amazon DynamoDB.
- Audio playback and download from the frontend.

The Polly Voice application is now fully integrated and ready for end-to-end testing in the next section.