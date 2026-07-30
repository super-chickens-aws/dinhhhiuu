+++
title = '5.8.1 Authentication with Amazon Cognito'
weight = 8

[params]
  collapsibleMenu = true
+++

## Authentication with Amazon Cognito

Security is an essential part of every cloud application. In Polly Voice, user authentication is implemented using **Amazon Cognito**, allowing users to securely register, sign in, and access protected resources without managing authentication infrastructure manually.

Amazon Cognito handles user identity management and issues JWT tokens that are used to authenticate subsequent API requests.

---

## Authentication Flow

The authentication process follows these steps:

1. A user registers or signs in through the frontend application.
2. Amazon Cognito validates the user's credentials.
3. After successful authentication, Cognito returns JWT tokens.
4. The frontend stores the tokens securely.
5. The Access Token is included in the Authorization header of every API request.
6. API Gateway validates the JWT before invoking AWS Lambda.

> 📷 **Screenshot:** Authentication Flow Diagram

---

## User Registration

Users can create an account using:

- Email address
- Password

Amazon Cognito verifies the user's credentials and creates a new account in the configured User Pool.

If email verification is enabled, the user must confirm the account before signing in.

> 📷 **Screenshot:** Amazon Cognito User Pool

---

## User Sign-In

Registered users authenticate using their email and password.

After successful authentication, Amazon Cognito issues:

- ID Token
- Access Token
- Refresh Token

These tokens are automatically used by the application during authenticated sessions.

> 📷 **Screenshot:** Successful User Login

---

## Protected Resources

Only authenticated users are allowed to access protected application features, including:

- Generate speech using Amazon Polly.
- View conversion history.
- Download generated audio files.

Unauthenticated users are redirected to the Login page before accessing these resources.

> 📷 **Screenshot:** Protected Dashboard

---

## Benefits of Amazon Cognito

Using Amazon Cognito provides several advantages:

- Fully managed user authentication service.
- Secure JWT-based authentication.
- Integration with Amazon API Gateway.
- Scalable identity management.
- No need to manage authentication servers.
- Supports future integration with social identity providers.

---

## Expected Result

After configuring Amazon Cognito:

- Users can register and sign in securely.
- JWT tokens are generated automatically.
- Protected pages require authentication.
- Only authenticated users can access backend APIs.
- Authentication is fully managed by AWS without storing user credentials inside the application.