+++
title = "1.7 Week 7 - System Integration and Application Deployment"
weight = 7

[params]
  collapsibleMenu = true
+++

## Objectives

During the seventh week, I completed the user interface, integrated all system components, and deployed the application to the Cloud environment. The objective was to ensure that the Frontend, Backend, and AWS services worked together seamlessly and that the application was ready for use.

---

## 7.1 Completing the User Interface

After completing the Backend functionalities, I continued developing the user interface using React.

The interfaces developed included:

- Registration page.
- Login page.
- Text-to-Speech page.
- Navigation Bar.
- Result display area.

In addition, I improved the layout to make the application easier and more intuitive for users.

---

## 7.2 Completing the Text-to-Speech Feature

Next, I finalized the user interface for the Text-to-Speech feature.

The following functionalities were added:

- Text input.
- Voice selection.
- Engine selection.
- Audio format selection.
- Audio playback after synthesis.
- Audio file download.

In addition, I implemented error messages and processing status indicators to improve the overall user experience.

![Image description](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog50.png)

---

## 7.3 Connecting the Frontend to the Backend

After completing the user interface, I connected the React application to the Serverless Backend.

The tasks included:

- Sending HTTP requests to Amazon API Gateway.
- Receiving responses from AWS Lambda.
- Displaying results on the user interface.
- Handling errors when the API returned invalid responses.

After completing the integration, the entire Text-to-Speech feature could be used directly from the web interface.

---

## 7.4 Integrating Amazon Cognito

Next, I integrated the user authentication system into the application interface.

The implemented features included:

- User registration.
- Email verification.
- User login.
- User logout.
- Authentication status checking.

After a successful login, the Access Token was used to call APIs that required authentication.

---

## 7.5 Calling Protected APIs

After Amazon Cognito was working correctly, I added the Access Token to the HTTP request headers.

Example:

```text
Authorization: Bearer <Access Token>
```

Amazon API Gateway uses a JWT Authorizer to validate the Access Token before forwarding the request to AWS Lambda.

Through this implementation, I completed the API protection mechanism for the system.

## 7.6 Deploying the Application with AWS Amplify

After completing all application features, I deployed the Frontend using AWS Amplify.

The deployment process included the following steps:

- Connecting AWS Amplify to GitHub.
- Selecting the project repository.
- Choosing the deployment branch.
- Configuring the build command.
- Setting the build output directory.
- Deploying the application.

After the deployment process was completed, AWS Amplify automatically provided a public URL that allowed users to access the application over the Internet.

![Image description](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog51.png)

---

## 7.7 Configuring Environment Variables

To enable the Frontend to communicate with the Backend, I configured the required environment variables in AWS Amplify.

The configured variables included:

- Amazon API Gateway URL.
- User Pool ID.
- App Client ID.
- AWS Region.

Managing these settings through Environment Variables makes it easier to maintain different configurations for development and production environments without modifying the application source code directly.

![Image description](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog52.png)

---

## 7.8 System Testing

After successfully deploying the application, I conducted end-to-end testing to verify that all components of the system worked together correctly.

The testing process included the following scenarios:

- User registration.
- Email verification.
- User login.
- User logout.
- Text-to-Speech conversion.
- Audio playback.
- Audio file download.
- Accessing protected APIs.

The results showed that all major features functioned correctly according to the system design.

---

## 7.9 Continuous Deployment with GitHub

In addition to the initial deployment, I explored the **Continuous Deployment** feature provided by AWS Amplify.

Whenever the source code is pushed to the configured GitHub branch:

- AWS Amplify automatically downloads the latest source code.
- Builds the application.
- Deploys the new version.

This automation makes application updates faster and reduces the amount of manual deployment work required.

---

## 7.10 Challenges Encountered

During the integration and deployment process, I encountered several challenges when connecting the Frontend to the Backend because the API Gateway endpoint URL and environment variables needed to be configured correctly.

In addition, synchronizing the configuration between Amazon Cognito, API Gateway, and AWS Amplify required careful verification to ensure that the authentication process continued to work properly after deployment.

---

## 7.11 Solutions

To resolve these issues, I reviewed the Environment Variables configuration, verified the API Gateway endpoint, and redeployed the application whenever configuration changes were made.

In addition, I performed end-to-end testing, from user login to using the Text-to-Speech feature, to quickly identify and resolve any issues that occurred during integration.

---

## 7.12 Knowledge Gained

After completing the seventh week, I achieved the following:

- Completed the user interface using React.
- Integrated the Frontend with the Serverless Backend.
- Used Access Tokens to call protected APIs.
- Understood the application deployment process using AWS Amplify.
- Learned how to manage Environment Variables.
- Understood the Continuous Deployment workflow with GitHub.
- Successfully completed the integration of the entire system.

---

## 7.13 Self-Assessment

The seventh week marked the completion and integration phase of the entire system. Successfully connecting the Frontend with the Backend and deploying the application through AWS Amplify helped me gain a deeper understanding of the process of moving a web application from a development environment to a production environment.

Through this experience, I became familiar with deployment workflows, configuration management, and post-deployment system testing. These are essential skills for developing and operating cloud-based applications on the AWS platform.