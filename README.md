# 🚀 Deploying a Web Application to AWS EC2 Using Bitbucket Pipelines

This guide outlines the streamlined process to automatically deploy a web application to an AWS EC2 instance using **Bitbucket Pipelines**, with resources integrated from **AWS S3**, **EC2**, **IAM**, and **CodeDeploy**.

### 🔍 Brief Explanation of Services Used

- **EC2 (Elastic Compute Cloud):** A scalable virtual server where the web application is hosted.
- **S3 (Simple Storage Service):** A secure object storage service used to store and retrieve deployment artifacts.
- **IAM (Identity and Access Management):** Controls access and permissions across AWS services, ensuring secure operations.
- **CodeDeploy:** An AWS service that automates application deployments to EC2 or on-premises servers.
- **CodeDeploy Agent:** A lightweight agent installed on EC2 to receive deployment commands from CodeDeploy.
- **Bitbucket:** A Git-based source code repository for managing your application code.
- **Bitbucket Pipelines:** A CI/CD tool built into Bitbucket for automating builds, tests, and deployments.
- **Repository Variables:** Securely store configuration values or secrets used in your pipeline YAML file.

### ✅ Deployment Workflow (Step-by-Step)

     **Create an S3 bucket and an EC2 instance**

- The S3 bucket stores application artifacts (code bundles).
- EC2 serves as the target machine where the application will be deployed.

**Create an IAM role for EC2 with permissions for S3 and CodeDeploy**

- This allows EC2 to securely interact with S3 and CodeDeploy during deployments.

**Attach AWS managed policies**

- `AmazonS3FullAccess`: Grants full access to S3 resources.
- `AWSCodeDeployFullAccess`: Grants permissions needed for CodeDeploy operations.

**Modify the IAM role of the EC2 instance**

- Attach the created IAM role to your EC2 instance via the AWS Console or CLI.


**Install the CodeDeploy agent on EC2 (from AWS documentation)**

- The agent enables the instance to communicate with the AWS CodeDeploy service.

**Verify the CodeDeploy agent status**

- Use `systemctl status codedeploy-agent` to confirm the agent is active and running.


**In AWS, navigate to CodeDeploy and create a new application**

- This is the container for your deployment configuration.


**Create a deployment group and an IAM role for CodeDeploy**

- The deployment group defines which EC2 instances receive the code.
- The IAM role allows CodeDeploy to manage deployments to those instances.

**Install a web server (e.g., NGINX) on the EC2 instance**

- This ensures the EC2 instance can serve your web application after deployment.

**Push your application code to Bitbucket**

- Ensure the repository includes an `appspec.yml` and deployment scripts.

**Define repository variables in Bitbucket Settings > Repository Variables**

- Store values like `S3_BUCKET`, `DEPLOYMENT_GROUP`, and `APPLICATION_NAME` securely.

**Enable Bitbucket Pipelines and commit code**

- On every push to the repository, the pipeline is triggered, automatically deploying changes to the EC2 instance — reflected live in the browser.

Pipeline successful executed in bit bucket.

With public IP on browser hosted the website

When changed and pushed again the changes are displayed successfully
