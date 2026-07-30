+++
title = '5.7.5 Test Error Handling'
weight = 5

[params]
  collapsibleMenu = true
+++

## Test Error Handling

Besides verifying normal application functionality, we should also ensure that the Polly Voice application can properly handle invalid requests and unexpected situations.

Proper error handling improves user experience, protects backend services, and helps developers troubleshoot issues more efficiently.

---

## Test Scenario

Verify how the application responds under the following conditions:

- User submits an empty text.
- User submits text exceeding the supported limit.
- Unauthorized API request.
- Invalid API endpoint.
- Internal server error.

---

## Test 1. Empty Input

Open the Polly Voice application.

Leave the text area empty and click **Generate**.

The application should display a validation message without sending a request to the backend.

Example message:

```text
Please enter some text before generating speech.
```

> 📷 **Screenshot:** Empty Input Validation

---

## Test 2. Exceed Maximum Text Length

Enter a text that exceeds the application's supported character limit.

Click **Generate**.

The application should reject the request and display an appropriate error message.

Example:

```text
Input text exceeds the maximum allowed length.
```

No audio file should be generated.

> 📷 **Screenshot:** Maximum Length Validation

---

## Test 3. Unauthorized Request

Sign out of the application.

Attempt to access a protected feature or directly invoke the API without a valid JWT token.

The API should return an authentication error.

Example response:

```http
401 Unauthorized
```

This confirms that Amazon Cognito JWT authorization is working correctly.

> 📷 **Screenshot:** Unauthorized Request

---

## Test 4. Invalid API Request

Modify the frontend API endpoint to an invalid URL (or send a request to a non-existent API route).

The application should display an appropriate error message instead of crashing.

Example:

```text
Unable to connect to the server.
Please try again later.
```

> 📷 **Screenshot:** Invalid API Endpoint

---

## Test 5. Verify CloudWatch Error Logs

If an error occurs during request processing:

1. Open the **AWS Management Console**.
2. Navigate to **Amazon CloudWatch**.
3. Open the log group for **PollyVoiceFunction**.
4. Review the latest log stream.

Verify that:

- Error details are recorded.
- Stack traces are available for debugging.
- Lambda execution information is logged correctly.

> 📷 **Screenshot:** CloudWatch Error Logs

---

## Expected Result

The error handling mechanism is considered successful if:

- Empty input is rejected before sending a backend request.
- Invalid input displays clear validation messages.
- Unauthorized users cannot access protected APIs.
- Invalid API requests are handled gracefully.
- Errors are recorded in Amazon CloudWatch Logs.
- The application remains stable without unexpected crashes.

These tests confirm that the Polly Voice application can properly handle common error scenarios while maintaining security, reliability, and a good user experience.