+++
title = '5.6.2 Configure Environment Variables'
weight = 2

[params]
  collapsibleMenu = true
+++

## Configure Environment Variables

In this section, we will configure the environment variables required by the React application.

Instead of hard-coding AWS resource information into the source code, the frontend reads configuration values from environment variables during the build process. This approach improves security, simplifies maintenance, and allows the same application to be deployed across different environments.

The Polly Voice application requires configuration values for Amazon Cognito and Amazon API Gateway.

---

## Why Environment Variables?

Environment variables allow the application to access AWS resources without modifying the source code.

Some benefits include:

- Separating configuration from application code.
- Simplifying deployment across multiple environments.
- Preventing hard-coded AWS resource identifiers.
- Making future updates easier without changing the application logic.

---

## Step 1 – Open Environment Variables

1. Open the **AWS Amplify Console**.
2. Select the **Polly Voice** application.
3. Choose the **Hosting** tab.
4. Select **Environment variables**.

> **Screenshot:** Open Environment Variables

---

## Step 2 – Add Cognito Configuration

Add the following environment variables.

| Variable | Description |
|----------|-------------|
| `VITE_REGION` | AWS Region |
| `VITE_USER_POOL_ID` | Amazon Cognito User Pool ID |
| `VITE_USER_POOL_CLIENT_ID` | Cognito App Client ID |

Example:

| Variable | Example Value |
|----------|---------------|
| `VITE_REGION` | `us-east-1` |
| `VITE_USER_POOL_ID` | `us-east-1_xxxxxxxxx` |
| `VITE_USER_POOL_CLIENT_ID` | `6xxxxxxxxxxxxxxxxxxxxx` |

These values are used by the React application to authenticate users through Amazon Cognito.

> **Screenshot:** Cognito Environment Variables

---

## Step 3 – Add Backend Configuration

Next, configure the backend API endpoint.

| Variable | Description |
|----------|-------------|
| `VITE_API_URL` | Amazon API Gateway Endpoint |

Example:

```text
https://xxxxxxxxxx.execute-api.us-east-1.amazonaws.com
```

The frontend sends authenticated HTTP requests to this endpoint whenever a user generates speech.

> **Screenshot:** API Gateway Environment Variable

---

## Step 4 – Review Configuration

Verify that all required variables have been added.

Example:

| Variable | Status |
|----------|--------|
| `VITE_REGION` | Configured |
| `VITE_USER_POOL_ID` | Configured |
| `VITE_USER_POOL_CLIENT_ID` | Configured |
| `VITE_API_URL` | Configured |

> **Screenshot:** Environment Variables List

---

## Step 5 – Save Changes

Choose **Save**.

AWS Amplify automatically detects that the application configuration has changed and starts a new deployment.

The deployment process includes:

- Installing project dependencies.
- Building the React application.
- Injecting the environment variables.
- Publishing the updated website.

> **Screenshot:** Amplify Build Started

---

## Verify

After the deployment finishes, verify that:

- All environment variables are listed in the Amplify Console.
- The build completes successfully.
- The application is deployed without errors.
- The frontend can access the configured AWS resources.

The application status should display:

```text
Build Successful
Deploy Successful
```

> **Screenshot:** Successful Deployment

---

## Result

We have successfully configured the environment variables required by the Polly Voice frontend.

The React application can now:

- Connect to Amazon Cognito for user authentication.
- Send authenticated requests to Amazon API Gateway.
- Communicate with the serverless backend without exposing sensitive configuration in the source code.

In the next section, we will build and deploy the frontend application through AWS Amplify.