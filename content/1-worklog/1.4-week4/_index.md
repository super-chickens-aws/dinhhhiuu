+++
title = "1.4 Week 4 - Building a Serverless Backend"
weight = 4

[params]
  collapsibleMenu = true
+++

## Objectives

During the fourth week, I began building the Backend for the project using a Serverless architecture on the AWS platform. The objective was to understand the Serverless model, deploy AWS Lambda functions, build HTTP APIs using Amazon API Gateway, and establish a foundation that allows the Frontend services to communicate with the system.

---

## 4.1 Understanding the Serverless Architecture

Before starting Backend development, I studied the **Serverless** architecture.

Serverless is a cloud computing model that allows developers to focus on building and deploying application functionality without managing servers or the underlying infrastructure. Resource provisioning, system scaling, and server maintenance are handled by the Cloud service provider.

In the Serverless model:

- AWS is responsible for managing the infrastructure and servers.
- Resources are automatically provisioned when requests are received.
- The system automatically scales based on the number of incoming requests.
- Users are charged only for the number of function executions and execution time.

To better understand this model, I compared the traditional application deployment architecture with the Serverless architecture.

| Criteria | Traditional Server Model | Serverless Model |
|----------|--------------------------|------------------|
| Server management | Developers or administrators manage the servers | AWS manages the entire infrastructure |
| Application deployment | Install and configure applications on servers | Only deploy the function source code |
| Scalability | Manual scaling or custom configuration | Automatically scales based on traffic |
| Cost | Charged based on server running time | Charged based on the number of executions and execution time |
| System maintenance | Update the operating system, apply patches, and perform maintenance manually | AWS performs maintenance automatically |
| Deployment time | Longer because servers must be prepared | Faster because only the function needs to be deployed |
| Suitable for | Systems requiring full server control or continuous operation | APIs, Microservices, Event Processing, and applications with variable traffic |

Through this section, I realized that the Serverless architecture significantly reduces the workload related to infrastructure management while optimizing costs for applications with unpredictable traffic. This is also why I chose **AWS Lambda** to build the Backend of the project during my internship.

---

## 4.2 Designing the Backend Architecture

Before writing the source code, I designed the overall Backend architecture.

The system consists of the following components:

- React Frontend
- Amazon API Gateway
- AWS Lambda
- Amazon Polly (implemented in the following weeks)

The request flow is designed as follows:

```text
Frontend
      │
      ▼
API Gateway
      │
      ▼
Lambda
      │
      ▼
Business Logic
```

This architecture allows the Frontend to simply call HTTP APIs without needing to know how the Backend is implemented.

---

## 4.3 Creating an AWS Lambda Function

After completing the architecture design, I created my first Lambda function.

Steps:

**Lambda → Create Function**

Then configure:

- Function Name
- Runtime (Node.js)
- Architecture
- Execution Role

After the function is successfully created, AWS provides an interface for editing and deploying the source code directly.

![Image Description](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog37.png)

---

## 4.4 Configuring the IAM Role for Lambda

To allow the Lambda function to access AWS services, I configured an IAM Role.

During this process, I learned about:

- Execution Role
- Permission Policy
- Trust Relationship

I also attached the required permissions so that the Lambda function could operate correctly.

For example:

- CloudWatch Logs
- Amazon Polly

To add permissions:

**Role name → Add permissions → Attach Policies / Create inline policy**

Through this section, I understood that AWS Lambda does not use Access Keys for authentication. Instead, it uses an IAM Role to securely access AWS services.

![Image Description](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog38.png)

## 4.5 Writing the Lambda Source Code

After successfully creating the Lambda function, I began writing the first processing logic to become familiar with how Lambda receives requests and returns responses.

At this stage, I implemented a simple function that returns the message **"Hello from Lambda"**. This served as a basic test to verify that the Lambda function could execute successfully before developing more complex features.

The source code is shown below:

```javascript
export const handler = async (event) => {
    return {
        statusCode: 200,
        headers: {
            "Content-Type": "application/json"
        },
        body: JSON.stringify({
            message: "Hello from Lambda"
        })
    };
};
```

### Source Code Explanation

The program above consists of the following main components:

| Component | Purpose |
|-----------|---------|
| `handler` | The function invoked by AWS Lambda when a request is received |
| `event` | Contains the data sent from API Gateway or other AWS services |
| `statusCode` | The HTTP status code returned to the client |
| `headers` | Specifies the response headers |
| `body` | The response content, converted into a JSON string |

When executed successfully, the Lambda function returns the following response:

```json
{
  "statusCode": 200,
  "headers": {
    "Content-Type": "application/json"
  },
  "body": "{\"message\":\"Hello from Lambda\"}"
}
```

Through this example, I understood the basic structure of an AWS Lambda function, how Lambda returns data using the standard HTTP response format, and how API Gateway can receive the response and send it back to the Frontend application.

---

# 4.6 Deploying the Lambda Function

After completing the source code, I deployed the Lambda function.

Steps:

- Modify the source code.
- Click **Deploy**.
- AWS updates the latest version of the Lambda function.

After the deployment is completed successfully, the Lambda function is ready to receive requests from Amazon API Gateway.

![Image Description](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog39.png)

---

## 4.7 Testing the Lambda Function

After completing the source code, I tested the Lambda function using the built-in **Test** feature available in the AWS Management Console.

The steps are as follows:

1. Open the details page of the **AWS Lambda** function.
2. Click the **Test** button in the upper-right corner.
3. The first time you use this feature, AWS prompts you to create a **Test Event**.
4. Enter a name for the Test Event (for example, `test-event`).
5. Keep the default sample event provided by AWS.
6. Click **Save**.
7. Click **Test** again to execute the function.

![Image Description](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog40.png)

---

### Execution Result

After the test completes successfully, AWS displays information such as:

- **Status:** The execution status (Succeeded or Failed).
- **Response:** The response returned by the Lambda function.
- **Execution duration:** The execution time.
- **Memory used:** The amount of memory consumed.

Example response:

```json
{
  "statusCode": 200,
  "headers": {
    "Content-Type": "application/json"
  },
  "body": "{\"message\":\"Hello from Lambda\"}"
}
```

If the function executes successfully, the status will be displayed as **Succeeded**, and the returned response will match the programmed output.

![Image Description](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog41.png)

---

### Viewing Execution Logs

After each execution, AWS Lambda automatically records execution logs in **Amazon CloudWatch Logs**.

This allows me to monitor the execution process, identify errors if any occur, and support debugging during development.

By testing the function directly in the AWS Management Console, I confirmed that the Lambda function was working correctly and was ready to be integrated with Amazon API Gateway in the following steps.

## 4.5 Writing the Lambda Source Code

After successfully creating the Lambda function, I began writing the first processing logic to become familiar with how Lambda receives requests and returns responses.

At this stage, I implemented a simple function that returns the message **"Hello from Lambda"**. This served as a basic test to verify that the Lambda function could execute successfully before developing more complex features.

The source code is shown below:

```javascript
export const handler = async (event) => {
    return {
        statusCode: 200,
        headers: {
            "Content-Type": "application/json"
        },
        body: JSON.stringify({
            message: "Hello from Lambda"
        })
    };
};
```

### Source Code Explanation

The program above consists of the following main components:

| Component | Purpose |
|-----------|---------|
| `handler` | The function invoked by AWS Lambda when a request is received |
| `event` | Contains the data sent from API Gateway or other AWS services |
| `statusCode` | The HTTP status code returned to the client |
| `headers` | Specifies the response headers |
| `body` | The response content, converted into a JSON string |

When executed successfully, the Lambda function returns the following response:

```json
{
  "statusCode": 200,
  "headers": {
    "Content-Type": "application/json"
  },
  "body": "{\"message\":\"Hello from Lambda\"}"
}
```

Through this example, I understood the basic structure of an AWS Lambda function, how Lambda returns data using the standard HTTP response format, and how API Gateway can receive the response and send it back to the Frontend application.

---

# 4.6 Deploying the Lambda Function

After completing the source code, I deployed the Lambda function.

Steps:

- Modify the source code.
- Click **Deploy**.
- AWS updates the latest version of the Lambda function.

After the deployment is completed successfully, the Lambda function is ready to receive requests from Amazon API Gateway.

![Image Description](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog39.png)

---

## 4.7 Testing the Lambda Function

After completing the source code, I tested the Lambda function using the built-in **Test** feature available in the AWS Management Console.

The steps are as follows:

1. Open the details page of the **AWS Lambda** function.
2. Click the **Test** button in the upper-right corner.
3. The first time you use this feature, AWS prompts you to create a **Test Event**.
4. Enter a name for the Test Event (for example, `test-event`).
5. Keep the default sample event provided by AWS.
6. Click **Save**.
7. Click **Test** again to execute the function.

![Image Description](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog40.png)

---

### Execution Result

After the test completes successfully, AWS displays information such as:

- **Status:** The execution status (Succeeded or Failed).
- **Response:** The response returned by the Lambda function.
- **Execution duration:** The execution time.
- **Memory used:** The amount of memory consumed.

Example response:

```json
{
  "statusCode": 200,
  "headers": {
    "Content-Type": "application/json"
  },
  "body": "{\"message\":\"Hello from Lambda\"}"
}
```

If the function executes successfully, the status will be displayed as **Succeeded**, and the returned response will match the programmed output.

![Image Description](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog41.png)

---

### Viewing Execution Logs

After each execution, AWS Lambda automatically records execution logs in **Amazon CloudWatch Logs**.

This allows me to monitor the execution process, identify errors if any occur, and support debugging during development.

By testing the function directly in the AWS Management Console, I confirmed that the Lambda function was working correctly and was ready to be integrated with Amazon API Gateway in the following steps.

## 4.13 Challenges Encountered

During the Backend development process, I encountered several challenges while becoming familiar with the Serverless architecture, especially understanding how Lambda receives data from API Gateway and returns responses in the required format.

In addition, configuring the IAM Role and integrating Lambda with API Gateway required careful verification to avoid permission issues or integration errors.

---

## 4.14 Solutions

To resolve these issues, I referred to the official AWS documentation, reviewed the execution logs in Amazon CloudWatch to identify the causes of errors, and tested the system after each configuration change.

In addition, I developed and tested each API individually before adding more features, making the development and testing process easier and more manageable.

---

## 4.15 Knowledge Gained

After completing the fourth week, I was able to:

- Understand the Serverless architecture on AWS.
- Master the process of creating and deploying AWS Lambda functions.
- Configure IAM Roles for Lambda.
- Understand the structure of an HTTP API.
- Create and manage APIs using Amazon API Gateway.
- Integrate API Gateway with Lambda.
- Test APIs and monitor execution through Amazon CloudWatch Logs.

---

## 4.16 Self-Evaluation

The fourth week marked the transition from learning AWS services to building the actual Backend for the project. By implementing AWS Lambda and Amazon API Gateway, I gained a deeper understanding of how to build a Serverless system and how the different components work together within the architecture.

The knowledge and experience gained during this week provide a solid foundation for integrating Amazon Cognito for user authentication and Amazon Polly for the Text-to-Speech feature in the following weeks.