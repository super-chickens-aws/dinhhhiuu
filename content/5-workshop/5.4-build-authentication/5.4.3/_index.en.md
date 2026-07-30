+++
title = '5.4.3 Configure Domain, Sign-in Options, OAuth and Hosted UI'
weight = 3

[params]
  collapsibleMenu = true
+++

## Configure Domain, Sign-in Options, OAuth and Hosted UI

After creating the User Pool and App Client, we need to configure the authentication settings for our application.

In this section, we will configure:

- Sign-in options
- User Pool domain
- OAuth 2.0 settings
- Hosted UI configuration

These settings enable Amazon Cognito to authenticate users securely and issue JWT tokens that can later be used to access protected backend APIs.

---

## Step 1 – Configure Sign-in Options

Open the **Amazon Cognito Console**.

Navigate to:

**User Pool → Sign-in experience**

Verify that the following settings are configured:

| Setting | Value |
|----------|-------|
| Sign-in identifier | Email |
| Username | Disabled |
| Multi-factor authentication (MFA) | Optional or Disabled |
| Self-registration | Enabled |

Using email as the primary sign-in identifier provides a simpler and more user-friendly authentication experience.

> **Insert screenshot of the Sign-in experience page.**

---

## Step 2 – Configure Password Recovery

Navigate to:

**User Pool → Sign-in experience → Password recovery**

Configure the recovery method:

| Setting | Value |
|----------|-------|
| Recovery method | Email only |

This allows users to reset their password through a verification email if they forget their credentials.

> **Insert screenshot of the Password recovery configuration.**

---

## Step 3 – Configure the User Pool Domain

Navigate to:

**Applications → Domain**

Click **Create Cognito domain**.

Enter a unique domain prefix.

Example:

```
pollyvoice-demo
```

Amazon Cognito automatically generates a Hosted UI domain similar to:

```
https://pollyvoice-demo.auth.ap-southeast-1.amazoncognito.com
```

This domain hosts the authentication pages provided by Amazon Cognito.

> **Insert screenshot of the Domain configuration page.**

---

## Step 4 – Configure OAuth Settings

Navigate to:

**Applications → App clients**

Select the **PollyVoiceWeb** App Client.

Under **Login pages**, configure the following settings.

### Allowed Callback URLs

```
http://localhost:5173
```

### Allowed Sign-out URLs

```
http://localhost:5173
```

After deploying the application with AWS Amplify, replace these URLs with the production domain.

---

Enable the following OAuth settings:

| Setting | Value |
|----------|-------|
| Authorization grant type | Authorization Code Grant |
| OpenID Connect scopes | openid, email, profile |

The Authorization Code Grant flow is the recommended OAuth 2.0 flow for modern web applications because it provides enhanced security while supporting browser-based authentication.

> **Insert screenshot of the OAuth configuration page.**

---

## Step 5 – Test the Hosted UI

Navigate to the Hosted UI by opening the Cognito domain created earlier.

The login page should display:

- Sign In
- Sign Up
- Forgot Password

At this stage, no users have been created yet, but the Hosted UI should be accessible and ready for authentication.

> **Insert screenshot of the Hosted UI login page.**

---

## Step 6 – Save the Configuration

Review all authentication settings.

Confirm that:

- Email is used as the sign-in identifier.
- Self-registration is enabled.
- Password recovery is configured.
- The Cognito domain has been created.
- Callback URLs are correct.
- OAuth Authorization Code Grant is enabled.
- Required scopes are selected.

The authentication service is now ready for user registration and login.

---

## Expected Result

After completing this section, we have successfully configured the authentication settings for Amazon Cognito.

The User Pool now provides:

- Email-based authentication.
- Secure password recovery.
- A Hosted UI for user authentication.
- OAuth 2.0 support using the Authorization Code Grant flow.
- JWT token issuance for authenticated users.

These configurations prepare the authentication system for the next step, where we will create a test user and verify the login process.