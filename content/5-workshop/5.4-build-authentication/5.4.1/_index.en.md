+++
title = '5.4.1 Create an Amazon Cognito User Pool'
weight = 1

[params]
  collapsibleMenu = true
+++

In this section, we will create an Amazon Cognito User Pool to manage user authentication for the Polly Voice application.

Amazon Cognito provides a fully managed authentication service that allows users to register, sign in, and obtain JSON Web Tokens (JWT) without requiring us to build our own authentication server.

The User Pool created in this section will later be integrated with the React frontend and Amazon API Gateway.

---

## Objectives

After completing this section, we will have:

- An Amazon Cognito User Pool.
- Email-based user authentication.
- Password-based sign-in.
- A foundation for JWT authentication.

---

## Step 1 - Open Amazon Cognito

1. Sign in to the **AWS Management Console**.
2. Search for **Amazon Cognito**.
3. Open the Amazon Cognito service.
4. Select **User pools**.
5. Click **Create user pool**.

> **Screenshot:** Amazon Cognito Console

---

## Step 2 - Configure the User Pool

On the **Configure sign-in experience** page, configure the following options.

### Authentication providers

Select:

- Cognito user pool

### Sign-in options

Enable:

- Email

This allows users to authenticate using their email address.

> **Screenshot:** Configure Sign-in Experience

Click **Next**.

---

## Step 3 - Configure Security Requirements

On the **Configure security requirements** page, keep the default password policy.

Recommended settings:

- Minimum password length: 8 characters
- Require uppercase letters
- Require lowercase letters
- Require numbers
- Require special characters

For Multi-Factor Authentication (MFA), select:

- No MFA

Since Polly Voice is a demonstration project, MFA is not required.

> **Screenshot:** Security Requirements

Click **Next**.

---

## Step 4 - Configure Sign-up Experience

Configure the following options.

### Self-registration

Enable:

- Allow users to sign themselves up

### Required attributes

Select:

- Email

The email address will be used as the unique identifier for each user.

> **Screenshot:** Sign-up Experience

Click **Next**.

---

## Step 5 - Configure Message Delivery

For email delivery, keep the default configuration.

Amazon Cognito will automatically send verification emails using the default email provider.

No additional configuration is required for this workshop.

> **Screenshot:** Message Delivery

Click **Next**.

---

## Step 6 - Integrate Your App

On the **Integrate your app** page, configure the following information.

### User Pool Name

Enter:

```text
polly-voice-user-pool
```

### Hosted Authentication Pages

Keep the default configuration.

The Hosted UI is not required because authentication will be handled by the React application.

> **Screenshot:** Integrate Your App

Click **Next**.

---

## Step 7 - Review and Create

Review all configuration settings.

If everything is correct, click:

**Create user pool**

Amazon Cognito will take a few moments to provision the new User Pool.

> **Screenshot:** Review Configuration

---

## Expected Result

After successfully creating the User Pool, the Amazon Cognito dashboard should display information similar to the following.

```text
User Pool Name:
polly-voice-user-pool

Sign-in:
Email

Authentication:
Password

Status:
Active
```

> **Screenshot:** User Pool Overview

---

## Summary

In this section, we successfully created an Amazon Cognito User Pool that will be used to authenticate users of the Polly Voice application.

The User Pool now provides:

- Email-based authentication.
- User registration.
- Secure password management.
- JWT token generation.

In the next section, we will configure the App Client that allows the React application to communicate securely with Amazon Cognito.