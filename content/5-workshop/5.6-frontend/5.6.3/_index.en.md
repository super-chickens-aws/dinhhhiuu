+++
title = '5.6.3 Build and Deploy the Application'
weight = 3

[params]
  collapsibleMenu = true
+++

## Build and Deploy the Application

After connecting the GitHub repository and configuring the required environment variables, we are ready to build and deploy the Polly Voice application using AWS Amplify.

AWS Amplify automatically provisions the hosting environment, installs project dependencies, builds the React application, and publishes the generated static files. Every future commit pushed to the selected branch will trigger the same deployment workflow automatically.

---

## Deployment Workflow

```text
GitHub Repository
        │
        ▼
AWS Amplify
        │
        ├── Install Dependencies
        │
        ├── Build React Application
        │
        ├── Inject Environment Variables
        │
        └── Deploy Website
                 │
                 ▼
      Polly Voice Web Application
```

---

## Step 1 – Start Deployment

Open the **AWS Amplify Console**.

Select the **Polly Voice** application.

Choose the connected branch.

If this is the first deployment, Amplify automatically starts building the application.

Otherwise, choose **Redeploy this version** or push a new commit to GitHub to trigger a new deployment.

> **Screenshot:** Start Deployment

---

## Step 2 – Monitor the Build Process

AWS Amplify performs several stages automatically.

Typical stages include:

- Provision
- Build
- Deploy
- Verify

During the build phase, Amplify installs all required dependencies and executes the build commands defined in the build specification.

> **Screenshot:** Build Progress

---

## Step 3 – Review Build Logs

Select the current deployment job.

Open the **Build logs** tab.

Verify that the following steps complete successfully:

- Installing dependencies
- Running the build command
- Generating production assets
- Uploading build artifacts

A successful build should finish without any errors.

> **Screenshot:** Build Logs

---

## Step 4 – Wait for Deployment

After the build completes, Amplify automatically deploys the generated files to the hosting environment.

When deployment finishes, the application status changes to:

```text
Build Successful
Deployment Successful
```

A public HTTPS URL is generated automatically.

Example:

```text
https://main.xxxxxxxxx.amplifyapp.com
```

> **Screenshot:** Deployment Complete

---

## Step 5 – Open the Application

Choose the generated application URL.

The Polly Voice homepage should appear.

At this stage, the frontend application has been successfully deployed and is publicly accessible.

> **Screenshot:** Polly Voice Homepage

---

## Verify

Verify the following items:

- The application URL is accessible.
- HTTPS is enabled.
- The homepage loads successfully.
- Static assets such as JavaScript and CSS files are loaded correctly.
- No build or deployment errors are reported in AWS Amplify.

> **Screenshot:** Successfully Loaded Website

---

## Continuous Deployment

One of the key benefits of AWS Amplify is its built-in Continuous Integration and Continuous Deployment (CI/CD).

Whenever a new commit is pushed to the connected GitHub branch, Amplify automatically performs the following steps:

1. Pull the latest source code.
2. Install project dependencies.
3. Build the React application.
4. Deploy the latest version.
5. Publish the updated website.

This automation eliminates the need for manual deployment and ensures that the hosted application always reflects the latest source code.

> **Screenshot:** Automatic Deployment Workflow

---

## Result

We have successfully built and deployed the Polly Voice frontend using AWS Amplify.

The application is now hosted on AWS with automatic HTTPS, continuous deployment, and seamless integration with GitHub.

In the next section, we will configure the frontend authentication flow using Amazon Cognito, allowing users to securely sign up, sign in, and access protected features of the Polly Voice application.