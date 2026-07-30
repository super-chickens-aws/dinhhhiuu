+++
title = '5.6.1 Connect Repository to AWS Amplify'
weight = 1

[params]
  collapsibleMenu = true
+++

## Connect Repository to AWS Amplify

In this section, we will connect the Polly Voice source code repository to **AWS Amplify Hosting**.

AWS Amplify supports Continuous Integration and Continuous Deployment (CI/CD). Once connected to a Git repository, Amplify automatically builds and deploys the application whenever new changes are pushed to the selected branch.

This enables a modern deployment workflow without requiring manual uploads.

---

## Architecture

```text
GitHub Repository
        │
        ▼
AWS Amplify Hosting
        │
Automatic Build
        │
Automatic Deploy
        │
        ▼
React Application
```

---

## Step 1 – Open AWS Amplify

1. Sign in to the AWS Management Console.
2. Search for **AWS Amplify**.
3. Open the **AWS Amplify Console**.

> **Screenshot:** AWS Amplify Console

---

## Step 2 – Create a New App

Choose **Create new app**.

Under **Start building with Amplify**, select:

- **GitHub**

AWS Amplify also supports GitLab, Bitbucket, CodeCommit, and other Git providers, but this workshop uses GitHub.

> **Screenshot:** Create New App

---

## Step 3 – Connect GitHub

If this is the first time using Amplify with GitHub:

1. Choose **Connect GitHub**.
2. Sign in to your GitHub account.
3. Authorize AWS Amplify to access your repositories.

After authorization, return to the Amplify Console.

> **Screenshot:** Authorize GitHub

---

## Step 4 – Select Repository

Choose the repository containing the Polly Voice frontend.

Example:

| Setting | Value |
|---------|-------|
| Repository | `polly-voice` |
| Branch | `main` |

Choose **Next**.

> **Screenshot:** Select Repository and Branch

---

## Step 5 – Review Build Settings

AWS Amplify automatically detects that the project is a React application and generates the build configuration.

Review the build settings before continuing.

Example configuration:

```yaml
version: 1
frontend:
  phases:
    preBuild:
      commands:
        - npm install
    build:
      commands:
        - npm run build
  artifacts:
    baseDirectory: dist
    files:
      - '**/*'
  cache:
    paths:
      - node_modules/**/*
```

If the application is created using **Vite**, ensure that the output directory is set to:

```text
dist
```

Choose **Next**.

> **Screenshot:** Review Build Settings

---

## Step 6 – Save and Continue

Review the application configuration.

Choose **Save and deploy**.

AWS Amplify will begin provisioning the hosting environment and preparing the first deployment.

> **Screenshot:** Save and Deploy

---

## Verify

After completing the previous steps, verify that:

- The GitHub repository is successfully connected.
- The correct branch is selected.
- The build configuration is detected correctly.
- Amplify starts the first build automatically.

The application status should change to:

```text
Provisioning
        ↓
Building
        ↓
Deploying
```

> **Screenshot:** Deployment Status

---

## Result

We have successfully connected the Polly Voice repository to AWS Amplify.

From now on, every time changes are pushed to the selected GitHub branch, AWS Amplify will automatically:

- Pull the latest source code.
- Install project dependencies.
- Build the React application.
- Deploy the latest version.
- Publish the updated website.

This CI/CD workflow simplifies application deployment and ensures that the frontend is always synchronized with the latest source code.

In the next section, we will configure the environment variables required by the React application to communicate with Amazon Cognito and the backend API.