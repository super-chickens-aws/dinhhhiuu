+++
title = '5.4.4 Create a Test User'
weight = 4

[params]
  collapsibleMenu = true
+++

## Create a Test User

After configuring the User Pool, App Client, and authentication settings, we can create a test user to verify that Amazon Cognito is functioning correctly.

There are two common methods for creating users:

- Self-registration through the Sign Up page.
- Manual creation by an administrator using the AWS Management Console.

In this workshop, we will create a user manually through the AWS Console for testing purposes.

---

## Step 1 – Open the User Management Page

Sign in to the **AWS Management Console**.

Navigate to:

**Amazon Cognito → User Pools → PollyVoiceUserPool → Users**

Click **Create user**.

> **Insert screenshot of the Users page.**

---

## Step 2 – Enter User Information

Configure the user with the following information.

| Setting | Example Value |
|----------|---------------|
| Username | demo@example.com |
| Email | demo@example.com |
| Email verified | Enabled |
| Temporary password | PollyVoice@123 |

The email address will be used as the primary sign-in identifier for this application.

Enabling **Email verified** allows the user to log in immediately without completing an additional email verification step.

> **Insert screenshot of the Create User page.**

---

## Step 3 – Create the User

Review the information.

Click **Create user**.

Amazon Cognito creates the new account and stores it in the User Pool.

The user now appears in the list of registered users.

> **Insert screenshot showing the created user.**

---

## Step 4 – Change the Temporary Password

Because the account was created with a temporary password, the user must change it during the first login.

There are two ways to complete this step:

- Sign in through the Amazon Cognito Hosted UI.
- Sign in through the Polly Voice React application.

After entering the temporary password, Amazon Cognito prompts the user to choose a new permanent password.

Example:

| Field | Example |
|-------|----------|
| Temporary Password | PollyVoice@123 |
| New Password | PollyVoice@1234 |

After the password is changed successfully, the account status becomes **Confirmed**.

> **Insert screenshot of the Change Password page.**

---

## Alternative Method – Self Registration

If **Self-registration** is enabled, users can create their own accounts without administrator assistance.

The registration process includes:

1. Open the Sign Up page.
2. Enter an email address.
3. Create a password.
4. Receive a verification code by email.
5. Enter the verification code.
6. Complete the registration process.

This approach is commonly used in production environments because it allows users to register independently.

> **Insert screenshot of the Sign Up page (optional).**

---

## Verify the User Status

Return to:

**Amazon Cognito → User Pools → Users**

Confirm that the user status is:

| Property | Expected Value |
|----------|----------------|
| Email Verified | Yes |
| Account Status | Confirmed |

The account is now ready for authentication.

> **Insert screenshot showing the confirmed user status.**

---

## Expected Result

After completing this section, we have successfully created a test user in Amazon Cognito.

The test account is now able to:

- Sign in using the registered email address.
- Authenticate through the Polly Voice application.
- Receive JWT tokens after successful login.
- Access protected backend APIs in the following sections of this workshop.