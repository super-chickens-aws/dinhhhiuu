+++
title = '5.4 Build Authentication'
weight = 4

[params]
  collapsibleMenu = true
+++

## Build Authentication

Authentication is the first component we need to configure before developing the backend services.

In this section, we will create an Amazon Cognito User Pool to manage user authentication for the Polly Voice application. Amazon Cognito provides a fully managed identity service that supports user registration, sign-in, password recovery, and JWT token generation without requiring a custom authentication server.

After completing this section, we will have a working authentication system that can later be integrated with the React frontend and Amazon API Gateway.

---

## Workshop Objectives

In this section, we will:

- Create an Amazon Cognito User Pool.
- Configure the application client.
- Configure the hosted authentication settings.
- Create a test user.
- Verify that the authentication service is working correctly.

---

## Authentication Workflow

The authentication process used by Polly Voice is illustrated below.

```text
             User
               │
               ▼
      React Application
               │
               ▼
      Amazon Cognito
               │
      Authentication
               │
               ▼
        JWT Access Token
               │
               ▼
      Amazon API Gateway
               │
               ▼
         AWS Lambda
```

Only authenticated users are allowed to invoke the backend APIs.

The JWT access token issued by Amazon Cognito will later be validated by Amazon API Gateway before forwarding requests to AWS Lambda.

> **Screenshot:** Authentication Workflow Diagram

---

## Sections

This part of the workshop is divided into the following steps:

1. Create an Amazon Cognito User Pool.
2. Configure the App Client.
3. Configure Authentication Settings.
4. Create a Test User.
5. Verify User Authentication.

After completing these steps, the authentication system will be ready for integration with the backend services.

In the following section, we will begin by creating the Amazon Cognito User Pool using the AWS Management Console.