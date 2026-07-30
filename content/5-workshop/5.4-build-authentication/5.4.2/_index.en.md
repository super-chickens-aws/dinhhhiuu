+++
title = '5.4.2 Create an App Client'
weight = 2

[params]
  collapsibleMenu = true
+++

## Create an App Client

After creating the Amazon Cognito User Pool, we need to create an **App Client**.

The App Client represents our React web application and allows it to communicate securely with Amazon Cognito without requiring AWS credentials.

Since Polly Voice is a Single Page Application (SPA), we will configure a **Public Client** without generating a client secret.

---

## Why Use an App Client?

The App Client provides the connection between the frontend application and Amazon Cognito.

It is responsible for:

- Authenticating users.
- Receiving JWT tokens after successful login.
- Managing user sessions.
- Allowing the frontend to access protected backend APIs.

For browser-based applications, using a client without a secret is the recommended approach because client secrets cannot be securely stored in frontend code.

---

## Step 1 – Open the User Pool

1. Sign in to the **AWS Management Console**.
2. Open **Amazon Cognito**.
3. Select the **User Pool** created in the previous section.
4. Navigate to the **Applications** tab.

> **Insert screenshot of the Applications page.**

---

## Step 2 – Create an App Client

Click **Create app client**.

> **Insert screenshot of the Create App Client button.**

---

## Step 3 – Configure the Application

Configure the application with the following settings.

| Setting | Value |
|----------|-------|
| Application type | Single-page application (SPA) |
| Application name | PollyVoiceWeb |
| Generate client secret | No |

We choose **Single-page application (SPA)** because the frontend is developed using React and runs entirely in the user's browser.

A client secret is not generated because public web applications cannot securely store confidential credentials.

> **Insert screenshot of the application configuration page.**

---

## Step 4 – Configure Callback URLs

Configure the URLs that Amazon Cognito will use after authentication.

During local development:

| Setting | Value |
|----------|-------|
| Callback URL | http://localhost:5173 |
| Sign-out URL | http://localhost:5173 |

After deploying the application to AWS Amplify, these URLs should be updated to the production domain.

Example:

| Setting | Value |
|----------|-------|
| Callback URL | https://your-amplify-domain.amplifyapp.com |
| Sign-out URL | https://your-amplify-domain.amplifyapp.com |

> **Insert screenshot of the Callback URL configuration.**

---

## Step 5 – Review the Configuration

Review all settings before creating the application.

Confirm that:

- Application type is **Single-page application (SPA)**.
- No client secret is generated.
- Callback URL is configured correctly.
- Sign-out URL is configured correctly.

Click **Create app client**.

> **Insert screenshot of the Review page.**

---

## Step 6 – Record the App Client Information

After the application is created, Amazon Cognito provides an **App Client ID**.

Record the following information because it will be required when configuring the React application.

| Item |
|------|
| Region |
| User Pool ID |
| App Client ID |

These values will later be added to the frontend configuration.

> **Insert screenshot showing the App Client ID.**

---

## Expected Result

After completing this section, we have successfully created an Amazon Cognito App Client for the Polly Voice application.

The App Client is now able to:

- Authenticate users from the React application.
- Issue JWT access tokens and ID tokens.
- Manage user login sessions.
- Serve as the authentication client for the Polly Voice frontend.