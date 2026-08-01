---
title: "Connect the Frontend to Amazon Cognito"
date: 2026-07-30
weight: 2
chapter: false
pre: " <b> 5.5.2. </b> "
---

In this section, an Amazon Cognito User Pool is configured to manage user
accounts for Polly Voice. The React frontend uses Cognito to register users,
send email confirmation codes, sign users in, obtain an access token, and send
that token to the backend.

1. Open the Amazon Cognito Console: [Amazon Cognito Console](https://console.aws.amazon.com/cognito/). Verify that the selected Region is **Europe (Stockholm) – `eu-north-1`**, then
choose **User Pools** from the left navigation pane.

![Open Amazon Cognito](https://hieuthaihcmut.github.io/fcj-workshop-template//images/5-Workshop/5.4-DeployFrontend/5.4.2-cognito/01-open-cognito.png)
![Open Amazon Cognito](https://hieuthaihcmut.github.io/fcj-workshop-template//images/5-Workshop/5.4-DeployFrontend/5.4.2-cognito/01-open-cognito-2.png)

2. Choose **Create user pool** to create a new User Pool.

![Create user pool](https://hieuthaihcmut.github.io/fcj-workshop-template//images/5-Workshop/5.4-DeployFrontend/5.4.2-cognito/01-create-user-pool.png)

3. In the **Define your application** section, select:

**Single-page app (SPA)**.

The SPA application type is appropriate for the React frontend and creates an
App Client. Then enter the application name in **Name your application**. For
example:

```text
polly-voice
```

![Define the Cognito application](https://hieuthaihcmut.github.io/fcj-workshop-template//images/5-Workshop/5.4-DeployFrontend/5.4.2-cognito/02-define-application.png)

4. In **Options for sign-in identifiers**, keep only **E-mail**.

Polly Voice uses email as the registration and sign-in identifier. Removing
username and phone number avoids additional identity handling and phone number
verification. Under **Required attributes for sign-up**, select the `name`
attribute if the AWS Console allows additional attributes to be configured.
Email is already used as the sign-in identifier.

![Select email sign-in](https://hieuthaihcmut.github.io/fcj-workshop-template//images/5-Workshop/5.4-DeployFrontend/5.4.2-cognito/03-email-sign-in.png)

The frontend submits the following attributes during registration:

```text
email
name
```

5. Under **Add a return URL**, enter the Amplify domain obtained in Section
5.4.1:

```text
https://<branch>.<app-id>.amplifyapp.com
```

Then choose **Create user directory** to create the Cognito User Pool.

![Configure user attributes](https://hieuthaihcmut.github.io/fcj-workshop-template//images/5-Workshop/5.4-DeployFrontend/5.4.2-cognito/04-user-attributes1.png)

## Retrieve the Cognito Connection Information

1. After the User Pool has been created, open:

```text
Amazon Cognito
→ User pools
→ Newly created User Pool
→ Overview
```

Locate and record the **User Pool ID**. The value has the following format:

```text
eu-north-1_xxxxxxxxx
```

This value is used for:

```text
VITE_COGNITO_USER_POOL_ID
```

![Cognito User Pool ID](https://hieuthaihcmut.github.io/fcj-workshop-template//images/5-Workshop/5.4-DeployFrontend/5.4.2-cognito/06-user-pool-id.png)

7. Inside the User Pool, open:

```text
Applications
→ App clients
→ polly-voice
```

Locate and record the **Client ID**. This value is used for:

```text
VITE_COGNITO_CLIENT_ID
```

![Cognito App Client ID](https://hieuthaihcmut.github.io/fcj-workshop-template//images/5-Workshop/5.4-DeployFrontend/5.4.2-cognito/07-app-client-id.png)

10. Open the Amplify application `polly-voice`, then navigate to:

```text
Hosting
→ Environment variables
```

![Amplify environment variables](https://hieuthaihcmut.github.io/fcj-workshop-template//images/5-Workshop/5.4-DeployFrontend/5.4.2-cognito/08-amplify-environment-variables.png)

Choose **Manage variables** and add the following environment variables:

| Variable | Value | Description |
|---|---|---|
| `VITE_AWS_ENABLED` | `true` | Enables Cognito integration on the frontend. |
| `VITE_AWS_REGION` | `eu-north-1` | The Region containing the Cognito User Pool. |
| `VITE_COGNITO_USER_POOL_ID` | `eu-north-1_xxxxxxxxx` | The ID of the newly created User Pool. |
| `VITE_COGNITO_CLIENT_ID` | `<APP_CLIENT_ID>` | The ID of the `polly-voice` SPA App Client. |

Then choose **Save** to store the variables.

![Amplify Cognito environment variables](https://hieuthaihcmut.github.io/fcj-workshop-template//images/5-Workshop/5.4-DeployFrontend/5.4.2-cognito/10-amplify-environment-variables.png)

11. After saving the environment variables, open **Overview**, select the
correct **Production branch** that was previously built, and choose
**Redeploy this version**.

Redeployment is required because Vite embeds all `VITE_*` variables into the
JavaScript bundle during the build process. Simply saving the variables without
rebuilding causes the website to continue using the previous configuration.

![Redeploy the Amplify frontend](https://hieuthaihcmut.github.io/fcj-workshop-template//images/5-Workshop/5.4-DeployFrontend/5.4.2-cognito/11-redeploy-frontend.png)
![Redeploy the Amplify frontend](https://hieuthaihcmut.github.io/fcj-workshop-template//images/5-Workshop/5.4-DeployFrontend/5.4.2-cognito/11-redeploy-frontend1.png)

## Synchronize the Backend Configuration

12. The backend must validate JWTs issued by the same User Pool and App Client
used by the frontend. Verify the following Lambda environment variables:

```text
AWS_COGNITO_USER_POOL_ID
AWS_COGNITO_CLIENT_ID
AWS_COGNITO_ISSUER_URI
```

The Issuer URI has the following format:

```text
https://cognito-idp.eu-north-1.amazonaws.com/<USER_POOL_ID>
```

If the newly created User Pool or App Client differs from the current backend
configuration, update the SAM parameters and redeploy the backend. If the
frontend and backend use different User Pools, JWT validation will fail.

<!-- ![Lambda Cognito environment variables](https://hieuthaihcmut.github.io/fcj-workshop-template//images/5-Workshop/5.4-DeployFrontend/5.4.2-cognito/12-lambda-cognito-configuration.png) -->

## Test User Registration and Sign-In

13. Open the Amplify production website and choose **Sign up**. Enter:

- Display name
- Email
- A password that satisfies the password policy

After registration, the application displays the confirmation code form. The
confirmation code is sent by Cognito to the registered email address.

<!-- ![Register a Polly Voice account](https://hieuthaihcmut.github.io/fcj-workshop-template//images/5-Workshop/5.4-DeployFrontend/5.4.2-cognito/13-sign-up-form.png) -->

14. Enter the confirmation code and confirm the account. If the code has
expired or the email was not received, use the **Resend confirmation code**
feature.

The confirmation code form is displayed directly inside the application and
does not rely on a browser popup.

<!-- ![Confirm the email address](https://hieuthaihcmut.github.io/fcj-workshop-template//images/5-Workshop/5.4-DeployFrontend/5.4.2-cognito/14-confirm-email.png) -->

15. After confirming the account, sign in using the email address and password.
The sign-in is considered successful when:

- The header displays the user's name.
- The **Sign in** button changes to **Sign out**.
- The profile displays the Cognito Subject ID.
- TTS features become available according to the authenticated user limits.
- The History page can be accessed.

<!-- ![Cognito sign-in succeeded](https://hieuthaihcmut.github.io/fcj-workshop-template//images/5-Workshop/5.4-DeployFrontend/5.4.2-cognito/15-sign-in-success.png) -->

16. Open the Cognito Console and navigate to:

```text
User management
→ Users
```

Verify that the newly created user has the following status:

```text
CONFIRMED
```

<!-- ![Confirmed Cognito user](https://hieuthaihcmut.github.io/fcj-workshop-template//images/5-Workshop/5.4-DeployFrontend/5.4.2-cognito/16-confirmed-user.png) -->

17. Open **Developer Tools → Network**, call a protected endpoint such as
History, and verify that the request contains the following header:

```http
Authorization: Bearer <access-token>
```

Do not include the complete token in the report screenshots. Only keep the
header name visible or mask most of the token value.

<!-- ![Authenticated API request](https://hieuthaihcmut.github.io/fcj-workshop-template//images/5-Workshop/5.4-DeployFrontend/5.4.2-cognito/17-authenticated-request.png) -->

## Common Issues

| Error | Cause | Resolution |
|---|---|---|
| `User is not confirmed` | The user has not entered the confirmation code. | Switch to the confirmation form or resend the code. |
| `User does not exist` | The email belongs to a different User Pool. | Verify `VITE_COGNITO_USER_POOL_ID`. |
| `Incorrect username or password` | Incorrect email/password or the password has been changed. | Verify the credentials or perform a password reset if necessary. |
| `Invalid client` | Incorrect App Client ID or the client has a client secret. | Use a SPA App Client without a client secret. |
| API returns HTTP 401 | The frontend and backend use different User Pools or Client IDs. | Synchronize the Amplify environment variables and SAM parameters. |
| The website still uses the previous configuration | The variables were saved but the frontend was not rebuilt. | Redeploy the Amplify branch. |
| Confirmation email not received | Incorrect email address, the email is in the Spam folder, or the code has not been resent. | Verify the email address and use **Resend confirmation code**. |

## Result

Amazon Cognito has been successfully integrated with the Polly Voice frontend.
Users can register, confirm their email addresses, sign in, and sign out on the
Amplify-hosted website. The frontend obtains an access token from Cognito and
sends it to API Gateway. The backend validates the token to separate each
user's TTS/STT history based on the corresponding Cognito Subject ID.