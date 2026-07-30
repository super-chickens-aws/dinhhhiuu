+++
title = '5.1 Overview'
weight = 1

[params]
  collapsibleMenu = true
+++

## Overview

In this workshop, we will build **Polly Voice**, a cloud-native Text-to-Speech (TTS) web application using Amazon Web Services (AWS) Serverless technologies.

The application enables users to securely log in, convert text into natural-sounding speech using Amazon Polly, store generated audio files in Amazon S3, and manage conversion history through Amazon DynamoDB.

Rather than deploying and maintaining traditional servers, the entire application is built on fully managed AWS services, allowing automatic scaling, lower operational costs, and simplified infrastructure management.

The workshop demonstrates how multiple AWS services can be integrated into a complete cloud application following serverless architecture and AWS security best practices.

---

## Learning Objectives

After completing this workshop, we will be able to:

- Understand how to design a Serverless application on AWS.
- Configure Amazon Cognito for user authentication.
- Build REST APIs using Amazon API Gateway and AWS Lambda.
- Generate speech from text using Amazon Polly.
- Store audio files in Amazon S3.
- Store application metadata in Amazon DynamoDB.
- Deploy a React application using AWS Amplify.
- Protect APIs using JWT authentication.
- Apply IAM Least Privilege principles.
- Test and validate the complete application workflow.

---

## Workshop Architecture

The Polly Voice application consists of the following AWS services:

- AWS Amplify
- Amazon Cognito
- Amazon API Gateway
- AWS Lambda
- Amazon Polly
- Amazon S3
- Amazon DynamoDB

Each service is responsible for a specific part of the application while working together through a fully serverless architecture.