+++
title = '2. Proposal'
weight = 2

[params]
  collapsibleMenu = true
+++

## Polly Voice
A Serverless Text-to-Speech Application Powered by AWS

---

## 1. Project Overview

### Objective

Polly Voice is a web application designed to convert text into speech using Amazon Polly. Users can log into the system, enter text, select a preferred voice, and generate high-quality audio files that can be played online or downloaded.

The application is built entirely on a Serverless architecture using Amazon Web Services (AWS), which minimizes operational costs, provides scalability, and eliminates the need for server management.

---

## 2. Problem Statement

### Current Situation

Today, many users need Text-to-Speech (TTS) technology for learning, reading documents, content creation, or assisting visually impaired individuals. However:

- Many Text-to-Speech services require paid subscriptions.
- Some platforms do not provide comprehensive multilingual support.
- Building a traditional TTS system requires deploying and maintaining servers, which increases both development time and operational costs.

### Proposed Solution

Polly Voice utilizes Amazon Polly to generate high-quality synthesized speech. The system follows a Serverless architecture consisting of:

- Amazon Cognito for user authentication and management.
- React hosted on AWS Amplify.
- Amazon API Gateway for handling frontend requests.
- AWS Lambda for business logic processing.
- Amazon Polly for speech synthesis.
- Amazon S3 for storing generated MP3 files.
- Amazon DynamoDB for storing conversion history.

Users simply log in, enter text, choose a voice, and the system automatically generates an audio file.

### Benefits

- No server management required.
- Low operational cost.
- Easily scalable as the number of users increases.
- Fast processing performance.
- Reusable for future AI applications and educational projects.

---

## 3. Solution Architecture

![Architecture Diagram](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog53.png)

### AWS Services Used

- AWS Amplify: Hosts the React frontend application.
- Amazon Cognito: Handles user registration and authentication.
- Amazon API Gateway: Provides REST APIs.
- AWS Lambda: Executes backend business logic.
- Amazon Polly: Converts text into speech.
- Amazon S3: Stores generated audio files.
- Amazon DynamoDB: Stores speech generation history.

### System Workflow

1. Users authenticate through Amazon Cognito.
2. The frontend sends requests to Amazon API Gateway.
3. API Gateway invokes AWS Lambda.
4. Lambda calls Amazon Polly to synthesize speech.
5. The generated MP3 file is stored in Amazon S3.
6. Lambda records the conversion history in Amazon DynamoDB.
7. The audio file URL is returned to the frontend.
8. Users can play or download the generated audio file.

---

## 4. Timeline

### Phase 1

- Research Amazon Polly.
- Learn the Serverless architecture.
- Design the overall system.

### Phase 2

- Develop the backend.
- Create AWS Lambda functions.
- Integrate Amazon API Gateway.
- Connect with Amazon Polly.
- Store generated audio files in Amazon S3.

### Phase 3

- Develop the React frontend.
- Integrate Amazon Cognito.
- Connect the frontend with the backend.

### Phase 4

- Perform testing.
- Finalize the user interface.
- Deploy the application using AWS Amplify.

---

## 5. Budget

The application is developed using AWS Free Tier services during the development phase.

Estimated monthly cost for a small-scale deployment:

| Service | Monthly Cost |
|----------|--------------|
| Amazon Polly | ~0.20 USD |
| AWS Lambda | ~0.00 USD |
| Amazon API Gateway | ~0.01 USD |
| Amazon S3 | ~0.05 USD |
| Amazon DynamoDB | ~0.02 USD |
| AWS Amplify | ~0.10 USD |
| Amazon Cognito | ~0.00 USD |

**Estimated Total Cost:** approximately **0.38 USD per month**.

---

## 6. Risks

### Potential Risks

- Users may submit text exceeding the supported character limit.
- Amazon Polly Free Tier limitations.
- Excessive storage of audio files may increase Amazon S3 costs.
- User authentication failures.

### Mitigation Strategies

- Limit the number of characters per conversion request.
- Apply the IAM Least Privilege principle.
- Periodically delete or archive old audio files.
- Authenticate every API request using Amazon Cognito JWT tokens.

---

## 7. Expected Outcomes

Upon completion, the system will:

- Allow users to register and log in securely.
- Convert text into speech using Amazon Polly.
- Play and download generated MP3 files.
- Store speech conversion history.
- Be fully deployed on an AWS Serverless architecture.
- Be easily extendable with additional languages, voices, and AI services in the future.