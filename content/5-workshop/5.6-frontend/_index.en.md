+++
title = '5.6 Build Frontend'
weight = 6

[params]
  collapsibleMenu = true
+++

## Build Frontend

In this section, we will deploy the React frontend using **AWS Amplify Hosting** and connect it to the backend services created in the previous sections.

The frontend provides a user interface where authenticated users can:

- Sign in using Amazon Cognito.
- Enter text for speech synthesis.
- Select a voice.
- Generate speech using Amazon Polly.
- Play or download the generated MP3 file.
- View their conversion history.

The application is deployed entirely through AWS Amplify, providing automatic hosting, HTTPS, and continuous deployment.

---

## Architecture

```text
User
   │
   ▼
AWS Amplify Hosting
   │
React Application
   │
   ├────────► Amazon Cognito
   │
   └────────► API Gateway
                    │
                    ▼
                AWS Lambda
```

The frontend communicates directly with Amazon Cognito for authentication and sends authenticated requests to API Gateway.

---

## Sections

This chapter is divided into the following sections.

1. Connect Repository to AWS Amplify
2. Configure Environment Variables
3. Build and Deploy the Application
4. Configure Frontend Authentication
5. Connect API Gateway
6. Verify Frontend Deployment

By the end of this chapter, the complete Polly Voice web application will be accessible through an AWS Amplify URL.