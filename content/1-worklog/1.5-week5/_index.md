+++
title = "1.5 Week 5 - Building an Authentication System with Amazon Cognito"
weight = 5

[params]
  collapsibleMenu = true
+++

## Objectives

During the fifth week, I implemented the user authentication system for the application using Amazon Cognito. The objective was to build user registration and login features, integrate authentication into the React application, and protect APIs using the JWT Authorizer mechanism provided by Amazon API Gateway.

---

## 5.1 Learning about Amazon Cognito

**Amazon Cognito** is AWS's identity management and user authentication service that enables developers to build user registration, login, and session management systems without having to develop a user database from scratch.

For Web and Mobile applications, Amazon Cognito provides built-in authentication, authorization, and user management mechanisms, helping reduce development time while improving system security.

During this learning process, I studied the main components of Amazon Cognito as follows:

| Component | Description |
|-----------|-------------|
| **User Pool** | Stores user information, manages user accounts, passwords, and authentication methods. It is responsible for handling user registration, login, and account management. |
| **App Client** | Represents an application that uses the User Pool for user authentication. Each application (Web, Mobile, etc.) is assigned a **Client ID** to connect with Cognito. |
| **Authentication** | The process of verifying a user's identity using login credentials such as Email, Username, and Password before granting access to the system. |
| **Authorization** | The process of determining a user's permissions after successful authentication. In this project, API Gateway uses JWT to verify whether a user is authorized to access the APIs. |
| **JSON Web Token (JWT)** | An encoded token containing user authentication information after a successful login. The JWT is included in every request sent to the Backend to prove that the user has been authenticated. |

By studying these components, I understood the basic Amazon Cognito authentication workflow:

1. The user registers or logs in through the application.
2. Amazon Cognito verifies the user's credentials.
3. If authentication succeeds, Cognito generates and returns **JWT Tokens**.
4. The application stores the tokens and includes them in subsequent requests to the Backend.
5. Amazon API Gateway uses a JWT Authorizer to validate the token before forwarding the request to AWS Lambda.

Through this topic, I understood that Amazon Cognito simplifies user management, reduces the workload involved in building authentication systems, and improves application security by using JSON Web Token (JWT)-based authentication.

---

## 5.2 Creating a User Pool

After learning about Amazon Cognito, I created a **User Pool** to manage user accounts and authentication for the application.

Steps performed:

**Amazon Cognito → User Pools → Create User Pool**

Then I configured the following basic settings:

- Authentication application: **Single-page application (SPA)**
- App client name
- Sign-in options
- Allowed callback URL
- Allowed sign-out URL

After completing the configuration, I selected **Create User Pool**.

The User Pool stores user accounts and provides registration, login, authentication, and session management features for the application.

![Image Description](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog46.png)

---

## 5.3 Creating an App Client

After creating the User Pool, I created an App Client so that the React application could communicate with Amazon Cognito.

Steps performed:

**User Pool → App Clients → Create App Client**

Then I configured:

- Application Type: SPA (Single-page Application)
- App Client Name
- Authentication Flow

After the configuration was completed, AWS generated a **Client ID**.

The Client ID is used when integrating Amazon Cognito with the React application.

![Image Description](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog47.png)

---

## 5.4 Configuring the Redirect URI

Next, I configured the Redirect URI to specify where Cognito should redirect users after they successfully complete the authentication process.

During development, I used the local address of the React application running on localhost.

When deploying the application to AWS Amplify, the Redirect URI was updated to the application's domain name.

Through this topic, I understood the role of the Redirect URI in the user authentication workflow.

---

## 5.5 Integrating Cognito with the React Application

After completing the Amazon Cognito configuration, I integrated user authentication into the React application.

First, I configured the User Pool and App Client information in the application so that React could communicate with Amazon Cognito.

The implementation included:

- Connecting the React application to Amazon Cognito.
- Configuring the User Pool ID and App Client ID.
- Building the user registration feature.
- Building the user login feature.
- Building the logout feature.
- Checking the user's authentication status.

Example configuration:

```javascript
export const authConfig = {
    userPoolId: "ap-southeast-1_xxxxxxxx",
    clientId: "3l8g0j7vxxxxxxxxxxxx"
};
```

After completing the configuration, the React application was able to use this information to perform user registration and login through Amazon Cognito.

## 5.6 Implementing the User Registration Feature

Next, I implemented the user registration functionality.

The registration process works as follows:

1. The user enters an email address and password.
2. React sends a registration request to Amazon Cognito.
3. Cognito creates a new user account.
4. Cognito sends a verification code to the user's email address.
5. The user enters the verification code to activate the account.

Example registration function:

```javascript
await register(email, password);
```

After successful registration, the application redirects the user to the verification page to complete the account activation process.

Through this implementation, I gained a clear understanding of Amazon Cognito's email verification process for user authentication.

---

## 5.7 Implementing the User Sign-in Feature

After activating the account, I proceeded to implement the sign-in functionality.

The authentication process works as follows:

1. The user enters an email address.
2. The user enters a password.
3. React sends a sign-in request to Amazon Cognito.
4. Cognito validates the user's credentials.
5. If the credentials are valid, Cognito returns a set of JWT tokens.

Example sign-in function:

```javascript
await login(email, password);
```

After a successful sign-in, the application receives the tokens issued by Amazon Cognito and stores the user's authenticated session.

These tokens are then included in requests to protected APIs managed by Amazon API Gateway.

Through this process, I learned how Amazon Cognito authenticates users and how JWT tokens are used to secure backend services.

---

## 5.8 Understanding JWT Tokens

After a successful sign-in, Amazon Cognito returns a set of authentication tokens.

I studied the three primary types of tokens provided by Cognito.

### ID Token

The ID Token contains information about the authenticated user, such as:

- User ID
- Email address
- Username

---

### Access Token

The Access Token is used to authenticate requests to protected APIs.

The frontend includes the Access Token in the HTTP request header when communicating with the backend.

---

### Refresh Token

The Refresh Token is used to obtain a new Access Token after the current one expires, allowing the user to remain signed in without logging in again.

Through this topic, I gained an understanding of how user sessions are managed in applications using Amazon Cognito.

---

## 5.9 Configuring the JWT Authorizer

After the sign-in functionality was working correctly, I proceeded to secure the application's APIs.

The configuration steps were:

**API Gateway → Authorization → Create Authorizer**

Then I configured:

- Authorizer Type: **JWT**
- Issuer
- Audience (App Client ID)

Next, I attached the JWT Authorizer to the API routes that required authentication.

With this configuration, Amazon API Gateway automatically validates the Access Token before forwarding the request to AWS Lambda.

---

## 5.10 Testing the Authentication System

After completing the authentication system, I performed a series of tests.

The testing scenarios included:

- Registering a new user account.
- Verifying the user's email address.
- Signing in.
- Calling protected APIs after authentication.
- Calling protected APIs without authentication.
- Testing invalid Access Tokens.
- Testing expired Access Tokens.

The test results confirmed that the APIs were protected correctly and that only authenticated users could access secured endpoints.

## 5.11 Challenges Encountered

During the implementation of the authentication system, I encountered several challenges while configuring the User Pool, App Client, and Redirect URI because these settings had to match the configuration of the React application.

In addition, integrating the JWT Authorizer with Amazon API Gateway required the Issuer and Audience values to be configured correctly so that API Gateway could successfully validate the Access Token.

---

## 5.12 Solutions

To resolve these issues, I carefully reviewed the configurations of the User Pool, App Client, and API Gateway while referring to the official AWS documentation.

In addition, I performed multiple test scenarios, including successful logins, failed login attempts, and invalid Access Tokens, to ensure that the authentication system functioned correctly and reliably.

---

## 5.13 Knowledge Gained

After completing the fifth week, I was able to:

- Understand the authentication mechanism of Amazon Cognito.
- Master the process of creating User Pools and App Clients.
- Integrate Amazon Cognito with a React application.
- Implement user registration and sign-in features.
- Understand the purposes of ID Tokens, Access Tokens, and Refresh Tokens.
- Configure a JWT Authorizer in Amazon API Gateway.
- Successfully protect APIs using JWT authentication.

---

## 5.14 Self-Evaluation

The fifth week helped me gain a comprehensive understanding of how to build a user authentication system on AWS. Integrating Amazon Cognito with React and Amazon API Gateway allowed me to understand how a modern authentication mechanism can be implemented without developing a user management system from scratch.

After completing this week's work, the application was capable of managing user accounts and protecting APIs using JWT authentication, providing a secure foundation for implementing the Text-to-Speech feature with Amazon Polly in the following week.