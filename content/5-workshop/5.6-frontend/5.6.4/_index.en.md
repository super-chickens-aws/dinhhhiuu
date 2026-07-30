+++
title = '5.6.4 Configure Frontend Authentication'
weight = 4

[params]
  collapsibleMenu = true
+++

## Configure Frontend Authentication

In this section, we will configure the React frontend to authenticate users using **Amazon Cognito**.

The frontend communicates directly with Amazon Cognito to allow users to register, confirm their accounts, sign in, and sign out. After a successful login, Amazon Cognito issues a JSON Web Token (JWT), which is included in every request sent to the backend API.

This authentication mechanism ensures that only authorized users can access the Text-to-Speech service.

---

## Authentication Flow

```text
User
   │
   ▼
React Application
   │
Sign In / Sign Up
   │
   ▼
Amazon Cognito
   │
Authenticate User
   │
Return JWT
   │
   ▼
React Application
   │
Authorization: Bearer <JWT>
   │
   ▼
Amazon API Gateway
```

---

## Step 1 – Configure Cognito Settings

Open the React project and configure the authentication settings using the environment variables created in the previous section.

The frontend should load the following values:

- AWS Region
- User Pool ID
- App Client ID

These values allow the application to communicate with the correct Amazon Cognito User Pool.

> **Screenshot:** Authentication Configuration

---

## Step 2 – Configure the Sign-Up Page

The application provides a registration page where new users can create an account.

The registration form includes:

- Email Address
- Password
- Confirm Password

When the user submits the form, the frontend sends the registration request to Amazon Cognito.

If the registration is successful, Cognito sends a verification code to the user's email address.

> **Screenshot:** Sign Up Page

---

## Step 3 – Configure Account Verification

After registration, users must verify their email address.

The verification page requests:

- Email Address
- Verification Code

The frontend sends the verification code to Amazon Cognito.

Once verified, the account becomes active and can be used to sign in.

> **Screenshot:** Email Verification Page

---

## Step 4 – Configure the Sign-In Page

The login page allows existing users to authenticate using:

- Email Address
- Password

If the credentials are correct, Amazon Cognito returns:

- Access Token
- ID Token
- Refresh Token

The frontend stores these tokens securely and uses the Access Token when communicating with the backend.

> **Screenshot:** Login Page

---

## Step 5 – Manage User Session

After a successful login, the frontend automatically retrieves the authenticated user's information.

The application maintains the user session until:

- The user signs out.
- The Access Token expires.
- The session is invalidated.

This allows users to continue using the application without logging in repeatedly during the active session.

> **Screenshot:** Authenticated User Session

---

## Step 6 – Configure Logout

The application also provides a logout function.

When the user selects **Logout**, the frontend:

1. Clears the stored authentication tokens.
2. Ends the current session.
3. Redirects the user to the login page.

This prevents unauthorized access after the user leaves the application.

> **Screenshot:** Logout Function

---

## Verify

After completing the authentication configuration, verify that the following workflow functions correctly.

### Register

- Create a new account.
- Receive the verification email.
- Confirm the account successfully.

> **Screenshot:** Successful Registration

---

### Login

Sign in using the registered account.

Expected result:

- Login succeeds.
- User information is displayed.
- JWT tokens are issued by Amazon Cognito.

> **Screenshot:** Successful Login

---

### Logout

Select **Logout**.

Expected result:

- Session is cleared.
- User is redirected to the login page.
- Protected pages are no longer accessible.

> **Screenshot:** Successful Logout

---

## Result

We have successfully configured frontend authentication using Amazon Cognito.

The Polly Voice application now supports:

- User registration
- Email verification
- Secure login
- Session management
- User logout
- JWT-based authentication

With authentication completed, users can securely access the application's protected features.

In the next section, we will connect the frontend to the backend API and implement the complete Text-to-Speech workflow.