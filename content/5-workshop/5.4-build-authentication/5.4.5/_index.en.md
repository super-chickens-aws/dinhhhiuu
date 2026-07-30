+++
title = '5.4.5 Sign In and Verify JWT Tokens'
weight = 5

[params]
  collapsibleMenu = true
+++

## Sign In and Verify JWT Tokens

In this section, we will verify that Amazon Cognito authentication is working correctly.

After a successful login, Amazon Cognito issues JSON Web Tokens (JWTs) that identify authenticated users. These tokens will later be used to authorize requests sent to the backend APIs.

---

## Authentication Flow

The authentication process is illustrated below.

```text
User
   │
   ▼
React Application
   │
   ▼
Amazon Cognito
   │
   ▼
Authenticate User
   │
   ▼
Issue JWT Tokens
   │
   ▼
React Application
```

> **Insert authentication flow diagram here.**

---

## Step 1 – Open the Polly Voice Application

Start the React application locally.

Example:

```
http://localhost:5173
```

The login page should be displayed.

> **Insert screenshot of the Login page.**

---

## Step 2 – Sign In

Enter the credentials created in the previous section.

Example:

| Field | Value |
|-------|-------|
| Email | demo@example.com |
| Password | PollyVoice@1234 |

Click **Sign In**.

If the credentials are correct, Amazon Cognito authenticates the user and redirects the application to the main dashboard.

> **Insert screenshot of a successful login.**

---

## Step 3 – Verify the User Session

After signing in successfully, verify that the application recognizes the authenticated user.

The dashboard should display information such as:

- User email
- Login status
- Logout button

This confirms that the authentication process has completed successfully.

> **Insert screenshot of the authenticated dashboard.**

---

## Step 4 – Verify JWT Tokens

Open the browser's Developer Tools.

Navigate to:

```
Application
    └── Local Storage
```

or

```
Application
    └── Session Storage
```

depending on the storage configuration used by the application.

Amazon Cognito stores several authentication tokens after login.

Typical stored values include:

- Access Token
- ID Token
- Refresh Token

> **Insert screenshot showing the stored tokens.**

---

## Understanding the JWT Tokens

Amazon Cognito generates three different tokens after a successful authentication.

### ID Token

The ID Token contains information about the authenticated user.

Typical information includes:

- User ID
- Email address
- User Pool ID
- Token expiration time

The frontend application uses this token to identify the current user.

---

### Access Token

The Access Token is used to authorize API requests.

When the frontend calls protected backend endpoints, the Access Token is included in the HTTP Authorization header.

Example:

```text
Authorization: Bearer <Access Token>
```

Amazon API Gateway validates this token before allowing access to AWS Lambda.

---

### Refresh Token

The Refresh Token allows the application to obtain new authentication tokens after the Access Token expires.

This enables users to remain signed in without entering their credentials repeatedly.

---

## Step 5 – Decode a JWT Token (Optional)

JWT tokens consist of three parts.

```text
Header
    .
Payload
    .
Signature
```

The Payload contains information such as:

- User identifier
- Email
- Issuer
- Expiration time

Developers can inspect the token payload during development to verify that authentication is working correctly.

> **Insert screenshot showing a decoded JWT payload (optional).**

---

## Step 6 – Sign Out

Click the **Logout** button.

After signing out:

- The user session is cleared.
- Authentication tokens are removed.
- Access to protected pages is revoked.
- The application returns to the Login page.

This verifies that the authentication lifecycle is functioning correctly.

> **Insert screenshot after logging out.**

---

## Expected Result

After completing this section, we have successfully verified the authentication process using Amazon Cognito.

The application is now able to:

- Authenticate users securely.
- Establish authenticated user sessions.
- Receive JWT tokens after login.
- Store authentication tokens for future API requests.
- Sign users out and terminate their sessions.

The authentication system is now fully operational and ready to secure the backend APIs in the next chapter.