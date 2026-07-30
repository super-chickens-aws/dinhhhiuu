+++
title = '5.8.2 Secure API using JWT Authorization'
weight = 8

[params]
  collapsibleMenu = true
+++

## Secure API using JWT Authorization

To prevent unauthorized access, all backend APIs in Polly Voice are protected using **JWT (JSON Web Token) Authorization** provided by Amazon Cognito.

Instead of allowing anonymous requests, every API call must include a valid JWT Access Token issued after the user successfully signs in.

Amazon API Gateway validates the token before forwarding the request to AWS Lambda.

---

## JWT Authorization Flow

The authorization process works as follows:

1. The user signs in through Amazon Cognito.
2. Amazon Cognito issues an Access Token.
3. The frontend stores the token.
4. Every request to API Gateway includes the token in the HTTP Authorization header.
5. API Gateway validates the token using the configured Cognito Authorizer.
6. Only valid requests are forwarded to AWS Lambda.

> 📷 **Screenshot:** JWT Authorization Flow

---

## Authorization Header

Each authenticated request includes the following HTTP header:

```http
Authorization: Bearer <Access_Token>
```

The Access Token is automatically attached by the frontend before sending requests to the backend.

---

## Configure Cognito Authorizer

To enable JWT authorization:

1. Open the **AWS Management Console**.
2. Navigate to **Amazon API Gateway**.
3. Select the Polly Voice HTTP API.
4. Open the **Authorization** section.
5. Create a new **JWT Authorizer**.
6. Configure:

- Authorizer Type: **JWT**
- Identity Source: `$request.header.Authorization`
- Issuer: Amazon Cognito User Pool
- Audience: Cognito App Client ID

Save the configuration.

> 📷 **Screenshot:** API Gateway JWT Authorizer

---

## Protect API Routes

After creating the JWT Authorizer:

1. Open the **Routes** page.
2. Select the protected endpoints.

For example:

- POST `/tts`
- GET `/history`

3. Choose **Authorization**.
4. Select the configured JWT Authorizer.
5. Save the changes.

All protected routes now require a valid JWT token.

> 📷 **Screenshot:** Protected API Routes

---

## Unauthorized Requests

If a request is sent without a valid Access Token:

- API Gateway rejects the request immediately.
- AWS Lambda is **not invoked**.
- The client receives an authentication error.

Example response:

```http
HTTP/1.1 401 Unauthorized
```

This reduces unnecessary Lambda executions and enhances application security.

> 📷 **Screenshot:** Unauthorized API Response

---

## Benefits of JWT Authorization

Using JWT authorization provides several advantages:

- Protects backend APIs from unauthorized access.
- Prevents anonymous requests from reaching AWS Lambda.
- Eliminates the need to implement authentication logic inside Lambda.
- Reduces unnecessary compute costs.
- Integrates seamlessly with Amazon Cognito.
- Improves overall application security.

---

## Expected Result

After configuring JWT authorization:

- Users must authenticate before accessing protected APIs.
- API Gateway validates every JWT Access Token.
- Invalid or expired tokens are rejected automatically.
- Only authorized requests are forwarded to AWS Lambda.
- Backend APIs remain secure without additional authentication code.    