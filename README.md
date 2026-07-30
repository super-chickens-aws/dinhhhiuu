# Test local
```
hugo server --baseURL=http://localhost:1313/
```

5.1 Overview

5.2 Prerequisites

5.3 Solution Architecture

5.4 Build Authentication
    5.4.1 Create User Pool
    5.4.2 Create App Client
    5.4.3 Configure Domain & OAuth
    5.4.4 Create Test User
    5.4.5 Verify Authentication

5.5 Build Backend
    5.5.1 Create DynamoDB
    5.5.2 Create S3 Bucket
    5.5.3 Create Lambda
    5.5.4 Configure API Gateway
    5.5.5 Connect Lambda with Polly, S3, DynamoDB
    5.5.6 Verify Backend

5.6 Build Frontend
    5.6.1 Create React Project
    5.6.2 Install Dependencies
    5.6.3 Configure Environment Variables
    5.6.4 Build Authentication Pages
    5.6.5 Build Text-to-Speech Interface
    5.6.6 Verify Deployment

5.7 Testing
    5.7.1 Test User Authentication
    5.7.2 Test Text-to-Speech API
    5.7.3 Test Audio Storage
    5.7.4 Test Conversion History
    5.7.5 Test Error Handling

5.8 Security
    5.8.1 Authentication with Amazon Cognito
    5.8.2 Secure API using JWT Authorization
    5.8.3 IAM Least Privilege
    5.8.4 Secure Amazon S3 Storage
    5.8.5 Security Best Practices

5.9 Clean Up Resources