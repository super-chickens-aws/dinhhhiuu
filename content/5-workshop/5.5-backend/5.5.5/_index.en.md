+++
title = '5.5.5 Configure JWT Authorization'
weight = 5

[params]
  collapsibleMenu = true
+++

## Configure JWT Authorization

In this section, we will secure the backend API using **Amazon Cognito JWT Authorizer**.

Instead of allowing anonymous requests, API Gateway will verify the JSON Web Token (JWT) issued by Amazon Cognito before forwarding any request to AWS Lambda.

Only authenticated users will be able to access the Text-to-Speech API.

---

## Architecture

```text
User
   │
Login
   │
   ▼
Amazon Cognito
   │
JWT Access Token
   │
   ▼
React Frontend
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
```

API Gateway validates the JWT before invoking the Lambda function. If the token is invalid or expired, the request is rejected automatically.

---

## Step 1 – Open the API

1. Open the **Amazon API Gateway Console**.
2. Select **polly-voice-api**.
3. In the left navigation pane, choose **Authorization**.

> **Screenshot:** Open Authorization page

---

## Step 2 – Create a JWT Authorizer

Choose **Create and attach authorizer**.

Configure the authorizer as follows.

| Setting | Value |
|---------|-------|
| Authorizer type | JWT |
| Name | `cognito-authorizer` |

> **Screenshot:** Create JWT Authorizer

---

## Step 3 – Configure Amazon Cognito

Under **Identity source**, enter:

```text
$request.header.Authorization
```

Under **Issuer URL**, select your Amazon Cognito User Pool.

API Gateway will automatically retrieve the issuer URL after the User Pool is selected.

Under **Audience**, select the App Client created earlier.

> **Screenshot:** Configure Cognito User Pool

---

## Step 4 – Attach the Authorizer

Navigate to **Routes**.

Select the route:

```text
POST /tts
```

Choose **Attach Authorizer**.

Select:

```text
cognito-authorizer
```

Save the changes.

> **Screenshot:** Attach JWT Authorizer to Route

---

## Step 5 – Deploy the API

Since this workshop uses the **$default** stage, the changes are deployed automatically.

If another stage is being used, deploy the API after saving the configuration.

> **Screenshot:** API deployed

---

## Verify

Open the route configuration and verify that:

- Authorization is enabled.
- JWT Authorizer is attached.
- The Cognito User Pool is selected.
- The App Client is configured correctly.

> **Screenshot:** Verify JWT Authorizer

---

## Test Unauthorized Access

Open **API Gateway → Test** (or use the frontend later).

Send a request without an Authorization header.

Expected result:

```text
401 Unauthorized
```

This confirms that anonymous users cannot access the API.

> **Screenshot:** Unauthorized request

---

## Test Authorized Access

Sign in to the application using Amazon Cognito.

After a successful login, obtain the Access Token.

The frontend automatically sends the following HTTP header:

```http
Authorization: Bearer eyJraWQiOi...
```

Send the request again.

Expected result:

```text
200 OK
```

The request is successfully forwarded to the Lambda function.

> **Screenshot:** Authorized request

---

## Result

We have successfully protected the backend API using Amazon Cognito JWT authentication.

From this point onward:

- Only authenticated users can access the API.
- JWT tokens are validated automatically by API Gateway.
- Invalid or expired tokens are rejected before reaching Lambda.
- Lambda only processes authenticated requests, improving the overall security of the Polly Voice application.

In the next section, we will implement the Lambda business logic to generate speech using Amazon Polly, upload audio files to Amazon S3, and store conversion history in Amazon DynamoDB.