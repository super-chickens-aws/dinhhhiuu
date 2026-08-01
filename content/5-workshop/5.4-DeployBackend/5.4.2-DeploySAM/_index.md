---
title: "Deploy the Backend with AWS SAM"
date: 2026-07-30
weight: 2
chapter: false
pre: " <b> 5.4.2. </b> "
---

AWS Serverless Application Model (AWS SAM) is used to describe, build, and
deploy the entire Polly Voice backend. SAM transforms `template.yaml` into a
CloudFormation stack so that the resources can be created and updated
consistently.

Backend architecture:

```mermaid
flowchart LR
    Client["React Frontend"]
    API["API Gateway<br/>HTTP API"]
    Lambda["AWS Lambda<br/>Node.js + Express"]
    Polly["Amazon Polly"]
    Transcribe["Amazon Transcribe"]
    S3[("Private Amazon S3")]
    DynamoDB[("Amazon DynamoDB")]
    CloudWatch["Amazon CloudWatch"]
    XRay["AWS X-Ray"]

    Client -->|HTTPS + JWT| API
    API --> Lambda
    Lambda --> Polly
    Lambda --> Transcribe
    Lambda --> DynamoDB
    Lambda --> CloudWatch
    Lambda --> XRay
    Polly --> S3
    Transcribe --> S3
```

1. Verify that the AWS CLI is authenticated to the correct account and region:

```powershell
aws sts get-caller-identity
aws configure get region
```

The Account ID must match the workshop account and the region must be:

```text
eu-north-1
```

<!-- ![Verify AWS identity](/images/5-Workshop/5.3-DeployBackend/5.3.2-sam/01-aws-identity.png) -->

{{% notice warning %}}
Do not deploy if `aws sts get-caller-identity` returns an old or incorrect AWS
account.
{{% /notice %}}

2. Open PowerShell in the `backend` directory and verify the deployment files:

```text
backend/
├── src/
│   ├── app.ts
│   ├── lambda.ts
│   ├── modules/
│   ├── infrastructure/
│   └── security/
├── package.json
├── package-lock.json
├── template.yaml
└── tsconfig.json
```

<!-- ![Backend source structure](/images/5-Workshop/5.3-DeployBackend/5.3.2-sam/02-backend-source.png) -->

3. Install the dependencies and verify the source:

```powershell
cd backend
npm ci
npm run typecheck
npm test
```

`npm ci` uses `package-lock.json` to create a reproducible dependency tree.
Type checking and tests run before the Lambda package is created.

<!-- ![Backend checks succeeded](/images/5-Workshop/5.3-DeployBackend/5.3.2-sam/03-backend-checks.png) -->

4. Validate the SAM template:

```powershell
sam validate
```

`template.yaml` declares:

- Lambda with Node.js 22 and the arm64 architecture.
- API Gateway HTTP API.
- DynamoDB table with on-demand billing.
- Private S3 media bucket.
- Lambda environment variables.
- IAM policies for Polly, Transcribe, S3, and DynamoDB.
- CloudWatch Logs and X-Ray tracing.

<!-- ![SAM validation succeeded](/images/5-Workshop/5.3-DeployBackend/5.3.2-sam/04-sam-validate.png) -->

5. Build the Lambda package:

```powershell
sam build --no-cached
```

SAM uses esbuild with this entry point:

```text
src/lambda.ts
```

A successful build creates artifacts under:

```text
backend/.aws-sam/build/
```

<!-- ![SAM build succeeded](/images/5-Workshop/5.3-DeployBackend/5.3.2-sam/05-sam-build.png) -->

{{% notice info %}}
If SAM cannot find esbuild, run `npm install` in the backend directory and
verify that `esbuild` is listed in `devDependencies`.
{{% /notice %}}

{{% notice warning %}}
If Windows reports `Access is denied` while SAM manages a temporary directory,
close processes holding the files, move the project outside a synchronized
OneDrive directory when necessary, and run `sam build --no-cached` again.
{{% /notice %}}

6. Prepare the deployment parameters:

| Parameter | Value |
|---|---|
| Stack name | `polly-voice-api` |
| Region | `eu-north-1` |
| MediaBucketName | `polly-voice-media-<ACCOUNT_ID>-eu-north-1` |
| HistoryTableName | `polly-voice-history` |
| CognitoUserPoolId | Cognito User Pool ID |
| CognitoClientId | SPA App Client ID |
| AllowedOrigins | `http://localhost:5173` for the first deployment |
| TranscribeLanguageCode | `en-US` |

An S3 bucket name must be globally unique. Adding the AWS Account ID reduces the
chance of a naming conflict.

<!-- ![Backend deployment parameters](/images/5-Workshop/5.3-DeployBackend/5.3.2-sam/06-deployment-parameters.png) -->

7. Run the first deployment:

```powershell
sam deploy --guided --capabilities CAPABILITY_IAM
```

Enter the prepared parameters. Use:

```text
Confirm changes before deploy: Y
Allow SAM CLI IAM role creation: Y
Disable rollback: N
Save arguments to configuration file: Y
```

`CAPABILITY_IAM` acknowledges that CloudFormation can create the Lambda
execution role from the policies in the SAM template. Lambda is not granted
`AdministratorAccess`.

<!-- ![SAM guided deployment](/images/5-Workshop/5.3-DeployBackend/5.3.2-sam/07-sam-deploy-guided.png) -->

8. SAM displays a CloudFormation change set before creating the resources.
Review the resources and confirm the deployment.

Main resource types:

```text
AWS::Serverless::HttpApi
AWS::Serverless::Function
AWS::S3::Bucket
AWS::DynamoDB::Table
AWS::IAM::Role
```

<!-- ![CloudFormation change set](/images/5-Workshop/5.3-DeployBackend/5.3.2-sam/08-change-set.png) -->

9. Wait for CloudFormation to complete. The stack must reach:

```text
CREATE_COMPLETE
```

SAM displays these Outputs:

```text
ApiUrl
FunctionName
MediaBucket
HistoryTable
```

<!-- ![SAM deployment completed](/images/5-Workshop/5.3-DeployBackend/5.3.2-sam/09-deployment-complete.png) -->

<!-- ![CloudFormation stack](/images/5-Workshop/5.3-DeployBackend/5.3.2-sam/10-cloudformation-stack.png) -->

10. Record `ApiUrl` from:

```text
AWS CloudFormation
→ Stacks
→ polly-voice-api
→ Outputs
```

The URL has this format:

```text
https://<API_ID>.execute-api.eu-north-1.amazonaws.com
```

The frontend uses:

```text
https://<API_ID>.execute-api.eu-north-1.amazonaws.com/api/v1
```

<!-- ![CloudFormation outputs](/images/5-Workshop/5.3-DeployBackend/5.3.2-sam/11-cloudformation-outputs.png) -->

## Permissions for Lambda to call AWS services

SAM creates the Lambda execution role from the `Policies` section:

```yaml
Policies:
  - DynamoDBCrudPolicy:
      TableName: !Ref HistoryTable
  - S3CrudPolicy:
      BucketName: !Ref MediaBucket
  - Statement:
      - Effect: Allow
        Action:
          - polly:SynthesizeSpeech
          - polly:DescribeVoices
          - transcribe:StartTranscriptionJob
          - transcribe:GetTranscriptionJob
          - transcribe:DeleteTranscriptionJob
        Resource: "*"
```

The AWS SDK in Lambda automatically receives temporary credentials from the
execution role. The project does not store an access key or secret access key
in the source or environment variables.

## Result

The backend is now deployed as a CloudFormation stack. API Gateway HTTP API,
Lambda, a private S3 bucket, and a DynamoDB table have been created in
`eu-north-1`. The stack Outputs provide the values required to test the backend
and connect the frontend.
