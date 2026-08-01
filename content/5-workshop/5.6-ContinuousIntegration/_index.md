---
title: "Setting Up the CI/CD Pipeline"
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

## 1. CI/CD Pipeline Overview

The Polly Voice CI/CD pipeline is divided into two components with distinct responsibilities. Continuous Integration (CI) verifies source code quality through unit testing, type checking, linting, building, and AWS SAM template validation. Continuous Deployment (CD) takes the version that has successfully passed the CI pipeline and deploys the backend to AWS.

The overall workflow is designed as follows:

```text
Developer
    ↓
GitHub
    ↓
Continuous Integration
    ↓
Test, typecheck, lint, build, and SAM validation
    ↓
Pull Request merged into main
    ↓
Continuous Deployment
    ↓
GitHub OIDC → Temporary AWS credentials
    ↓
SAM deploy → CloudFormation updates the backend
    ↓
Check the /health endpoint
```

GitHub Actions serves as the control plane that orchestrates the CI/CD workflow and is not involved in processing application requests at runtime. The pipeline covers the entire software delivery process, from source code validation and backend deployment to frontend protection, monitoring, and operational alerting.

## 2. Prerequisites

The following prerequisites are required for both the CI and CD pipelines:

| Component                 | Configuration                                     |
| ------------------------- | ------------------------------------------------- |
| AWS account               | AWS account used to manage and deploy the backend |
| GitHub repository         | `super-chickens-aws/polly-voice`                  |
| Deployment branch         | `main`                                            |
| Backend runtime           | Node.js 22                                        |
| Dependency manager        | npm                                               |
| Source code management    | Git                                               |
| Local AWS tools           | AWS CLI and AWS SAM CLI                           |
| Infrastructure management | AWS SAM and AWS CloudFormation                    |
| Automation platform       | GitHub Actions                                    |
| Backend Region            | `eu-north-1`                                      |
| Local AWS profile         | `polly-dev`                                       |
| Permissions               | Required IAM permissions for each deployment step |
| Application resources     | Existing Polly Voice resources                    |

The `polly-dev` AWS profile is used only for administrative tasks on the local development machine. Local access keys are never stored in GitHub Secrets. During automated deployments, GitHub Actions authenticates using OpenID Connect (OIDC) and obtains temporary AWS credentials instead of long-term access keys.

## 3. Continuous Integration Deployment

### Step 1 — Review the Repository Status

Before creating the workflow, the team reviewed the architecture documentation, Lambda source code, the AWS SAM template, the `package.json` files, the `lockfile`, and the TypeScript configuration. The objective was to ensure that the new pipeline accurately reflected the current architecture of the repository.

The development environment inspection showed that the repository was on the `lab/4.3-ci` branch. The machine was running Node.js `v24.15.0`, npm `11.12.1`, and AWS SAM CLI `1.164.0`. The SAM template confirmed that the backend uses the `nodejs22.x` runtime, the API type is `AWS::Serverless::HttpApi`, and the Lambda handler is `lambda.handler`.

![Polly Voice repository audit results](https://hieuthaihcmut.github.io/fcj-workshop-template/images/5-Workshop/5.5-ContinuousIntegration/00-repository-audit.png)

<p align="center">
    <strong>Figure 5.5.1.</strong> Repository audit showing the Git branch, tool versions, and AWS SAM configuration of the Polly Voice repository.
</p>

### Step 2 — Create the Repository CI Workflow

The `Repository CI` workflow was created in the application repository at:

```text
.github/workflows/ci.yml
```

Since the workflow only requires read access to the source code, it follows the principle of least privilege:

```yaml
permissions:
  contents: read
```

GitHub Actions installs Node.js 22 and uses `npm ci` to install dependencies, ensuring that the dependencies are installed exactly as specified in the lockfile. The backend validation steps are:

```bash
npm ci
npm test
npm run typecheck
npm run build
```

The frontend is validated using the following commands:

```bash
npm ci
npm run lint
npm run build
```

The infrastructure is validated and built using AWS SAM:

```bash
sam validate --lint --template-file backend/template.yaml
sam build \
  --template-file backend/template.yaml \
  --build-dir backend/.aws-sam/build-ci
```

Before installing dependencies, the workflow also checks for UTF-8 Byte Order Marks (BOM) and validates the syntax of YAML files. Optional configuration files, such as AWS Amplify configuration files, are validated only if they exist in the repository.

### Step 3 — Test the CI Workflow Locally

Before pushing the workflow to GitHub, the team executed the corresponding steps on the local development machine to verify that the backend, frontend, and AWS SAM template could successfully pass the validation pipeline.

```powershell
# Backend
Set-Location backend
npm.cmd ci
npm.cmd test
npm.cmd run typecheck
npm.cmd run build

# Frontend
Set-Location ../frontend
npm.cmd ci
npm.cmd run lint
npm.cmd run build

# AWS SAM
Set-Location ..
$env:PATH = "$(Resolve-Path backend/node_modules/.bin);$env:PATH"

sam validate --lint `
  --template-file backend/template.yaml

sam build `
  --template-file backend/template.yaml `
  --build-dir backend/.aws-sam/build-ci

# Check whitespace and formatting issues in Git changes
git diff --check
```

The local validation results are summarized below.

| Test ID | Description | Expected Result | Actual Result | Status |
|---|---|---|---|---|
| CI-LOCAL-01 | Run backend unit tests | All unit tests pass | 1 test file, 1 test passed | Passed |
| CI-LOCAL-02 | Backend type checking | No TypeScript errors | Exit code 0 | Passed |
| CI-LOCAL-03 | Build backend | TypeScript compilation succeeds | Exit code 0 | Passed |
| CI-LOCAL-04 | Lint frontend | No Oxlint errors | Exit code 0 | Passed |
| CI-LOCAL-05 | Build frontend | `dist` directory is generated | Vite build completed successfully | Passed |
| SAM-LOCAL-01 | Validate SAM template | Template is valid | SAM confirmed the template is valid | Passed |
| SAM-LOCAL-02 | Build SAM application | Build completes successfully | Displayed `Build Succeeded` | Passed |

### Step 4 — Verify CI with GitHub Actions

After the workflow was pushed to GitHub, both workflow executions triggered by the `push` and `pull_request` events completed successfully. The validation results are summarized below.

| Test ID | Description | Expected Result | Actual Result | Status |
|---|---|---|---|---|
| CI-GITHUB-01 | Verify workflow on push | Workflow completes successfully | `push` workflow passed | Passed |
| CI-GITHUB-02 | Verify workflow on Pull Request | Workflow completes successfully | `pull_request` workflow passed | Passed |

GitHub reported **All checks have passed** with two successful workflow checks. After both GitHub Actions checks completed successfully, Pull Request #3 was merged into the `main` branch.

![Pull Request #3 validation results](https://hieuthaihcmut.github.io/fcj-workshop-template/images/5-Workshop/5.5-ContinuousIntegration/01-pr-checks.png)

<p align="center">
    <strong>Figure 5.5.2.</strong> Both GitHub Actions checks completed successfully, and Pull Request #3 had no conflicts with the <code>main</code> branch before being merged.
</p>

### Step 5 — Merge the Workflow into the Main Branch

Pull Request #3 was merged using merge commit `3f638a3`. After updating the local repository, the `main` branch was synchronized with `origin/main`, and the `.github/workflows/ci.yml` file was confirmed to exist on the `main` branch. This indicates that the CI workflow has become part of the primary branch and can now serve as the foundation for implementing the Continuous Deployment (CD) pipeline.

![Pull Request #3 merged into main](https://hieuthaihcmut.github.io/fcj-workshop-template/images/5-Workshop/5.5-ContinuousIntegration/02-pr-merged.png)

<p align="center">
    <strong>Figure 5.5.3.</strong> Pull Request #3 was successfully merged into the <code>main</code> branch after all GitHub Actions checks completed successfully.
</p>

## 4. Implementing Continuous Deployment

### Step 6 — Configure the GitHub Deployment Environment

The team created a GitHub Environment named `dev` to separate deployment configuration from the workflow source code. This environment allows deployments only from the `main` branch, ensuring that every backend deployment originates from code that has successfully passed the Continuous Integration (CI) pipeline.

The deployment environment contains the following environment variables.

| Variable | Purpose |
|---|---|
| `AWS_REGION` | Specifies the deployment Region (`eu-north-1`) |
| `AWS_DEPLOY_ROLE_ARN` | Specifies the GitHub deployment IAM role |
| `CFN_EXECUTION_ROLE_ARN` | Specifies the CloudFormation execution role |
| `SAM_ARTIFACTS_BUCKET` | Specifies the S3 bucket used to store SAM deployment artifacts |
| `CFN_STACK_NAME` | Specifies the CloudFormation stack name (`polly-voice-api`) |
| `MEDIA_BUCKET_NAME` | Provides the name of the existing S3 media bucket |
| `HISTORY_TABLE_NAME` | Provides the name of the existing DynamoDB history table |
| `COGNITO_USER_POOL_ID` | Provides the Amazon Cognito User Pool ID |
| `COGNITO_CLIENT_ID` | Provides the Amazon Cognito App Client ID |
| `FRONTEND_ORIGIN` | Specifies the frontend origin allowed by the backend |

Managing these values through a GitHub Environment enables the workflow to be reused across different environments without hardcoding environment-specific configuration into the workflow file.

![GitHub Environment dev configuration](https://hieuthaihcmut.github.io/fcj-workshop-template/images/5-Workshop/5.5-ContinuousIntegration/07-github-environment-dev.png)

<p align="center">
    <strong>Figure 5.5.4.</strong> The GitHub Environment <code>dev</code> is restricted to the <code>main</code> branch and contains all variables required for the deployment process.
</p>

### Step 7 — Configure GitHub OIDC and IAM

GitHub Actions was configured to authenticate with AWS using OpenID Connect (OIDC) with the audience set to `sts.amazonaws.com`. Each time the workflow runs, GitHub obtains temporary AWS credentials without storing long-term access keys in GitHub Secrets.

Two IAM roles are separated according to their responsibilities.

| IAM Role | Responsibility |
|---|---|
| `polly-voice-github-deploy-dev` | Controls the deployment process initiated by GitHub Actions |
| `polly-voice-cfn-execution-dev` | Performs infrastructure changes managed by the CloudFormation stack |

The GitHub deployment role is used by the workflow to initiate the deployment process, while the CloudFormation execution role performs the infrastructure updates. This separation of responsibilities limits permissions according to each role and follows the principle of least privilege.

### Step 8 — Prepare AWS SAM Deployment

An Amazon S3 artifacts bucket in the `eu-north-1` Region is used to store deployment packages generated by AWS SAM. The bucket has **Block Public Access** enabled and uses default encryption to prevent deployment artifacts from being exposed publicly.

The SAM template receives the names of the existing DynamoDB table and S3 media bucket through template parameters. The stack does not recreate these data resources. Instead, the Lambda function receives the resource names through environment variables, while SAM policies grant permissions based on the provided resource names.

Before deployment, the template successfully passed all validation steps.

| Validation | Result |
|---|---|
| Backend unit tests | Passed |
| TypeScript type checking | Passed |
| Backend build | Passed |
| `sam validate` | Template is valid |
| `sam build` | Build completed successfully |

### Step 9 — Build the Continuous Deployment Workflow

The Continuous Deployment workflow is located at:

```text
.github/workflows/backend-deploy.yml
```

The workflow deploys to the GitHub Environment `dev` whenever backend changes are merged into the `main` branch. In addition to automatic deployment, the workflow also supports manual execution through `workflow_dispatch` when needed.

The successful deployment workflow consists of the following steps.

1. Check out the repository.
2. Set up Node.js 22.
3. Install the AWS SAM CLI.
4. Install backend dependencies using `npm ci`.
5. Run backend unit tests.
6. Perform TypeScript type checking.
7. Build the backend.
8. Validate the SAM template.
9. Build the SAM application.
10. Authenticate with AWS using GitHub OIDC.
11. Execute `sam deploy`.
12. Retrieve the `ApiUrl` output from CloudFormation.
13. Invoke the `/health` endpoint.
14. Generate the deployment summary.

GitHub OIDC provides temporary AWS credentials for the workflow. The CloudFormation execution role is passed to the deployment process, allowing CloudFormation to perform infrastructure changes on behalf of the workflow.

### Step 10 — Successfully Deploy the Backend

The backend deployment completed successfully with the following results.

| Property | Result |
|---|---|
| Environment | `dev` |
| Region | `eu-north-1` |
| Stack | `polly-voice-api` |
| CloudFormation stack status | `CREATE_COMPLETE` |
| Health check | `Passed` |

GitHub Actions obtained temporary AWS credentials through OIDC, after which AWS SAM packaged and deployed the backend application. AWS CloudFormation managed all application resources within the `polly-voice-api` stack. Once deployment was complete, the workflow retrieved the API URL from the stack outputs and invoked the `/health` endpoint to verify that the backend was operating correctly.

![GitHub Actions successfully deployed the backend](https://hieuthaihcmut.github.io/fcj-workshop-template/images/5-Workshop/5.5-ContinuousIntegration/09-backend-cd-success.png)

<p align="center">
    <strong>Figure 5.5.5.</strong> The CD workflow successfully deployed the backend to the <code>dev</code> environment and confirmed that the health check status was <code>Passed</code>.
</p>

![CloudFormation stack created successfully](https://hieuthaihcmut.github.io/fcj-workshop-template/images/5-Workshop/5.5-ContinuousIntegration/10-cloudformation-stack.png)

<p align="center">
    <strong>Figure 5.5.6.</strong> The <code>polly-voice-api</code> stack reached the <code>CREATE_COMPLETE</code> status in the <code>eu-north-1</code> Region.
</p>

![Health endpoint responded successfully](https://hieuthaihcmut.github.io/fcj-workshop-template/images/5-Workshop/5.5-ContinuousIntegration/11-health-check.png)

<p align="center">
    <strong>Figure 5.5.7.</strong> The <code>/health</code> endpoint returned the status <code>ok</code>, confirming that the <code>polly-voice-backend</code> service is running successfully in the <code>eu-north-1</code> Region.
</p>

### Step 11 — Protect the Frontend with AWS WAF

AWS WAF has been associated with the AWS Amplify Hosting application, and the firewall status has changed to `Enabled`. The Web ACL serves as a protective layer in front of the Amplify-hosted frontend, allowing incoming traffic to the application to be filtered and controlled. In this architecture, AWS WAF is associated with Amplify Hosting rather than directly with the API Gateway HTTP API.

![AWS WAF enabled for Amplify Hosting](https://hieuthaihcmut.github.io/fcj-workshop-template/images/5-Workshop/5.5-ContinuousIntegration/12-amplify-waf-enabled.png)

<p align="center">
    <strong>Figure 5.5.8.</strong> AWS WAF has been associated with the Amplify Hosting application, and the firewall status is <code>Enabled</code>.
</p>

### Step 12 — Create a CloudWatch Dashboard

The team created a CloudWatch Dashboard named `polly-voice-dev` to monitor the backend deployed in the `eu-north-1` Region. The dashboard aggregates the following metrics:

- Lambda Invocations
- Lambda Errors
- Lambda Average Duration
- Lambda Throttles
- HTTP API Count
- HTTP API 4xx Errors
- HTTP API 5xx Errors
- HTTP API Latency
- HTTP API Integration Latency

The dashboard provides a centralized view of traffic, errors, and performance metrics for both AWS Lambda and the API Gateway HTTP API after deployment.

![CloudWatch dashboard for the development environment](https://hieuthaihcmut.github.io/fcj-workshop-template/images/5-Workshop/5.5-ContinuousIntegration/13-cloudwatch-dashboard.png)

<p align="center">
    <strong>Figure 5.5.9.</strong> The <code>polly-voice-dev</code> dashboard consolidates operational metrics for AWS Lambda and the API Gateway HTTP API in the <code>eu-north-1</code> Region.
</p>

### Step 13 — Configure CloudWatch Alarms and Amazon SNS

An Amazon SNS topic named `polly-voice-alerts-dev` was configured with a confirmed email subscription. The email address is intentionally omitted from this report. Two CloudWatch Alarms use this SNS topic to send notifications whenever errors are detected. In addition, OK actions are also associated with the SNS topic to notify administrators when the system recovers.

| Alarm | Monitored Metric | Status Shown |
|---|---|---|
| `polly-voice-dev-lambda-errors` | AWS Lambda `Errors` | `INSUFFICIENT_DATA`, actions enabled |
| `polly-voice-dev-api-5xx` | API Gateway `5xx` errors | `INSUFFICIENT_DATA`, actions enabled |

The `INSUFFICIENT_DATA` status immediately after alarm creation indicates that there is not yet enough monitoring data to evaluate the alarm state. This is expected behavior and does not indicate a deployment failure. The configuration does not require intentionally generating system failures to trigger alarm notifications.

![CloudWatch alarms monitoring backend errors](https://hieuthaihcmut.github.io/fcj-workshop-template/images/5-Workshop/5.5-ContinuousIntegration/14-cloudwatch-alarms.png)

<p align="center">
    <strong>Figure 5.5.10.</strong> Two CloudWatch Alarms monitoring AWS Lambda Errors and API Gateway 5xx responses have been configured with alarm actions enabled and associated with the Amazon SNS topic <code>polly-voice-alerts-dev</code>.
</p>

## 5. Results

The Polly Voice system has successfully completed both the Continuous Integration (CI) and Continuous Deployment (CD) pipeline. The CI process validates source code quality before a Pull Request is merged, while the CD pipeline automatically deploys the backend after changes are merged into the `main` branch.

The main achievements include:

- GitHub OIDC eliminates the need to store long-term AWS access keys in GitHub.
- AWS SAM and AWS CloudFormation provide a repeatable and reliable infrastructure deployment process.
- The `polly-voice-api` CloudFormation stack reached the `CREATE_COMPLETE` status.
- The backend health check completed successfully.
- AWS WAF protects the frontend hosted on AWS Amplify Hosting.
- CloudWatch Dashboard provides a centralized view of backend operations.
- CloudWatch Alarms and Amazon SNS support system monitoring, error notifications, and recovery alerts.

The completed CI/CD and monitoring architecture is illustrated below.

```text
Developer
    ↓
GitHub
    ↓
Repository CI
    ↓
Merge into main
    ↓
Backend CD
    ↓
GitHub OIDC
    ↓
AWS SAM
    ↓
AWS CloudFormation
    ↓
API Gateway HTTP API and Lambda
    ↓
CloudWatch Dashboard, Alarms, and SNS
```

AWS WAF operates as a dedicated security layer protecting the frontend hosted on AWS Amplify Hosting.