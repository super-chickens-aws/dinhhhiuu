+++
title = "5. Workshop"
weight = 5

[params]
  collapsibleMenu = true
+++

## Overview

**Building the Polly Voice on AWS Serverless Architecture**

**Polly Voice** is a Text-to-Speech (TTS) web application built entirely on **Amazon Web Services (AWS)** using a **Serverless** architecture.

The application allows users to register an account, sign in, enter text, select a voice, and generate MP3 audio files using **Amazon Polly**. Once the speech synthesis process is complete, the generated audio files are stored in **Amazon S3**, while the conversion history is recorded in **Amazon DynamoDB**, allowing users to review or download their previous conversions at any time.

Throughout this workshop, the entire system will be deployed using fully managed AWS services, eliminating the need to manage servers, reducing operational costs, and enabling the application to scale easily as the number of users grows.

By completing this workshop, we will gain a comprehensive understanding of how multiple AWS services work together to build a complete cloud-native web application, covering user authentication, backend processing, data storage, and frontend deployment.

---

## Workshop Content

This workshop is divided into the following sections:

1. [Overview](5.1-Overview/)
2. [Prerequisites](5.2-Prerequisites/)
3. [Solution Architecture](5.3-Architecture/)
4. [Deploy Backend](5.4-Backend/)
5. [Deploy Frontend](5.5-Frontend/)
6. [End-to-End Testing](5.6-Testing/)
7. [Monitoring & Security](5.7-Monitoring/)
8. [Clean Up Resources](5.8-Cleanup/)

By the end of this workshop, we will have deployed a complete Text-to-Speech application that follows modern AWS cloud architecture and security best practices.