+++
title = '5.9 Clean Up Resources'
weight = 9

[params]
  collapsibleMenu = true
+++

## Clean Up Resources

After completing the workshop, we should delete all AWS resources created during the deployment to avoid unnecessary charges.

---

### Step 1: Delete the AWS Amplify Application

1. Open the **AWS Amplify Console**.
2. Select the **Polly Voice** application.
3. Choose **Delete App** and confirm the deletion.

> **Insert screenshot of deleting the Amplify application here.**

---

### Step 2: Delete the Amazon Cognito User Pool

1. Open the **Amazon Cognito Console**.
2. Select the User Pool created for this workshop.
3. Choose **Delete User Pool**.
4. Type the confirmation text and delete the resource.

> **Insert screenshot of deleting the Cognito User Pool here.**

---

### Step 3: Delete the Backend Resources

Delete the following services:

- AWS Lambda Function
- Amazon API Gateway

Navigate to each service in the AWS Console, select the resource, and choose **Delete**.

> **Insert screenshots of deleting Lambda and API Gateway here.**

---

### Step 4: Delete the Amazon S3 Bucket

1. Open the **Amazon S3 Console**.
2. Empty all objects in the bucket.
3. Delete the bucket.

> **Insert screenshot of deleting the S3 bucket here.**

---

### Step 5: Delete the Amazon DynamoDB Table

1. Open the **Amazon DynamoDB Console**.
2. Select the table used by Polly Voice.
3. Choose **Delete Table** and confirm.

> **Insert screenshot of deleting the DynamoDB table here.**

---

## Verification

Finally, review the AWS Console to ensure that all resources created during this workshop have been removed.

The following resources should no longer exist:

- AWS Amplify Application
- Amazon Cognito User Pool
- AWS Lambda Function
- Amazon API Gateway
- Amazon S3 Bucket
- Amazon DynamoDB Table

Removing these resources helps prevent unnecessary AWS charges and keeps the AWS account clean after completing the workshop.