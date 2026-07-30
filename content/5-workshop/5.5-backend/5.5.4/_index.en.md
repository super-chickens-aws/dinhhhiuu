+++
title = '5.5.4 Configure API Gateway'
weight = 4

[params]
  collapsibleMenu = true
+++

## Configure API Gateway

In this section, we will create an Amazon API Gateway HTTP API that exposes the backend services to the frontend application.

Instead of allowing the React application to invoke AWS Lambda directly, every request will pass through API Gateway. This provides a centralized entry point for authentication, authorization, routing, and request management.

The API will later be protected using Amazon Cognito JWT authentication.

---

## Architecture

```text
React Frontend
        │
 HTTPS Request
        │
        ▼
Amazon API Gateway
        │
        ▼
AWS Lambda
```

API Gateway receives HTTP requests from the frontend and forwards them to the appropriate Lambda function.

---

## Step 1 – Open API Gateway

1. Sign in to the AWS Management Console.
2. Search for **API Gateway**.
3. Open the **Amazon API Gateway Console**.

> **Screenshot:** Open Amazon API Gateway Console

---

## Step 2 – Create an HTTP API

Choose **Create API**.

Under **HTTP API**, choose **Build**.

HTTP API is selected because it offers lower latency, lower cost, and native support for JWT authentication.

> **Screenshot:** Select HTTP API

---

## Step 3 – Configure the API

Configure the API with the following values.

| Setting | Value |
|---------|-------|
| API name | `polly-voice-api` |
| Protocol | HTTP |
| Stage | `$default` |

Choose **Next**.

> **Screenshot:** Configure HTTP API

---

## Step 4 – Add Lambda Integration

Choose **Add integration**.

Select:

- Integration type: **Lambda**
- Lambda function: **polly-voice-backend**

Choose **Next**.

API Gateway will invoke this Lambda whenever a request is received.

> **Screenshot:** Add Lambda Integration

---

## Step 5 – Create Routes

Create the following route.

| Method | Route |
|---------|-------|
| POST | `/tts` |

This endpoint will receive text from the frontend and trigger Amazon Polly through Lambda.

> **Screenshot:** Create POST /tts route

---

## Step 6 – Review and Create

Review all configurations.

Choose **Create**.

Wait until the API is successfully deployed.

> **Screenshot:** API created successfully

---

## Verify

After the API is created, verify that:

- The HTTP API is active.
- The Lambda integration is attached.
- The POST `/tts` route exists.
- The API endpoint URL is displayed.

The endpoint URL will look similar to:

```text
https://xxxxxxxxxx.execute-api.us-east-1.amazonaws.com
```

This URL will be used later by the React frontend.

> **Screenshot:** HTTP API Endpoint

---

## Result

We have successfully created an Amazon API Gateway HTTP API.

The backend now exposes a REST endpoint that forwards requests to AWS Lambda.

In the next section, we will secure this API using Amazon Cognito JWT Authorizers so that only authenticated users can access the Text-to-Speech service.