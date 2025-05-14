# DevOps End-to-End Automation Project Guide

## 📚 Table of Contents
1. [Introduction](#introduction)
2. [AWS Authentication](#aws-authentication)
3. [Terraform Infrastructure](#terraform-infrastructure)
4. [Application Development](#application-development)
5. [CI/CD with GitHub Actions](#cicd-with-github-actions)
6. [Monitoring and Verification](#monitoring-and-verification)

## 🎯 Introduction

This guide walks you through setting up a complete DevOps pipeline, from infrastructure provisioning to application deployment. We'll cover:
- AWS authentication and security best practices
- Infrastructure as Code (IaC) with Terraform
- Container-based application deployment
- Continuous Integration and Deployment (CI/CD) with GitHub Actions

## ✅ AWS Authentication

### 📌 Theory: AWS Authentication Methods
AWS offers multiple authentication methods:
1. **Access Keys**: Long-term credentials (not recommended for production)
2. **IAM Roles**: Temporary credentials with specific permissions
3. **OIDC**: OpenID Connect for secure, token-based authentication
4. **AWS SSO**: Single Sign-On for enterprise environments

### 📌 Pre-requisites Check

1. **Install AWS CLI**:
```bash
# Ubuntu
sudo apt install awscli -y

# Mac
brew install awscli

# Verify installation
aws --version
```

2. **Configure AWS Credentials**:
```bash
# Configure credentials
aws configure

# Verify configuration
aws sts get-caller-identity
```

Expected output:
```json
{
    "UserId": "AIDAXXXXXXXXXXXXXXXX",
    "Account": "123456789012",
    "Arn": "arn:aws:iam::123456789012:user/your-username"
}
```

3. **AWS Console Verification**:
- Go to AWS Console → IAM → Users
- Verify your user exists and has appropriate permissions
- Check the "Security credentials" tab for active access keys

## ✅ Terraform Infrastructure

### 📌 Theory: Infrastructure as Code (IaC)
IaC allows you to:
- Version control your infrastructure
- Automate deployment and updates
- Ensure consistency across environments
- Implement security best practices

### 📌 Setup and Validation

1. **Install Terraform**:
```bash
# Ubuntu
sudo apt install unzip -y
wget https://releases.hashicorp.com/terraform/1.5.0/terraform_1.5.0_linux_amd64.zip
unzip terraform_1.5.0_linux_amd64.zip
sudo mv terraform /usr/local/bin/

# Mac
brew install terraform

# Verify installation
terraform -version
```

2. **Initialize Terraform Project**:
```bash
# Create project directory
mkdir aws-terraform-demo && cd aws-terraform-demo

# Initialize Terraform
terraform init
```

3. **AWS Console Verification**:
- Go to AWS Console → S3
- Verify bucket creation
- Check bucket permissions and settings
- Go to EC2 → Security Groups
- Verify security group rules
- Go to EC2 → Instances
- Verify instance creation and status

## ✅ Application Development

### 📌 Theory: Containerization
Containerization provides:
- Consistent runtime environment
- Isolation of dependencies
- Easy scaling and deployment
- Version control for applications

### 📌 Setup and Testing

1. **Create Dockerfile**:
```dockerfile
FROM python:3.9-slim

WORKDIR /app

# Install system dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    && rm -rf /var/lib/apt/lists/*

# Copy requirements and install Python dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy application code
COPY deduplication.py .

# Set environment variables
ENV PYTHONUNBUFFERED=1

# Run the application
CMD ["python", "deduplication.py"]
```

2. **Local Testing**:
```bash
# Build the image
docker build -t deduplication-processor .

# Run the container
docker run -d --name deduplication-processor deduplication-processor

# Check logs
docker logs deduplication-processor
```

## ✅ CI/CD with GitHub Actions

### 📌 Theory: CI/CD Pipeline
A CI/CD pipeline:
- Automates build and test processes
- Ensures code quality
- Deploys applications consistently
- Reduces manual intervention

### 📌 GitHub Actions Setup

1. **Workflow Configuration**:
```yaml
name: Build and Push Docker Image

on:
  push:
    branches: [ main ]
    paths:
      - 'lambdas/deduplication/**'
      - '.github/workflows/docker-build.yml'
  workflow_dispatch:  # Allow manual triggering

env:
  AWS_REGION: us-east-2
  ECR_REPOSITORY: deduplication-processor
  IMAGE_TAG: ${{ github.sha }}

permissions:
  id-token: write   # Required for OIDC
  contents: read    # Required for checkout

jobs:
  build-and-push:
    runs-on: ubuntu-latest
    steps:
      # ... (workflow steps as defined in docker-build.yml)
```

2. **GitHub Console Verification**:
- Go to your repository → Actions
- Check workflow runs and status
- Verify build logs and artifacts
- Monitor deployment status

3. **AWS Console Verification**:
- Go to ECR → Repositories
- Verify image tags and layers
- Check image scan results
- Go to ECS → Task Definitions
- Verify task definition updates

## ✅ Monitoring and Verification

### 📌 AWS CloudWatch
1. **Logs Verification**:
- Go to CloudWatch → Logs
- Check application logs
- Monitor error rates
- Set up log-based metrics

2. **Metrics Verification**:
- Go to CloudWatch → Metrics
- Monitor CPU and memory usage
- Check network metrics
- Set up alarms for critical metrics

### 📌 GitHub Actions Monitoring
1. **Workflow Insights**:
- Go to repository → Actions → Insights
- Check workflow duration
- Monitor success rates
- Analyze failure patterns

2. **Security Scanning**:
- Go to repository → Security
- Check dependency alerts
- Review code scanning results
- Monitor secret scanning

## 🔍 Troubleshooting Guide

### Common Issues and Solutions

1. **AWS Authentication Issues**:
```bash
# Check AWS credentials
aws sts get-caller-identity

# Verify IAM permissions
aws iam get-user
aws iam list-attached-user-policies --user-name YOUR_USERNAME
```

2. **Terraform State Issues**:
```bash
# Initialize Terraform
terraform init

# Check state
terraform state list

# Refresh state
terraform refresh
```

3. **Docker Build Issues**:
```bash
# Check Docker daemon
docker info

# Verify build context
docker build --no-cache -t test-image .
```

4. **GitHub Actions Issues**:
- Check workflow permissions
- Verify secrets configuration
- Review OIDC setup
- Check AWS role permissions

## 📚 Additional Resources

1. **AWS Documentation**:
- [AWS CLI Configuration](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-files.html)
- [IAM Best Practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)
- [ECS Task Definitions](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/task_definitions.html)

2. **Terraform Documentation**:
- [Terraform AWS Provider](https://registry.terraform.io/providers/hashicorp/aws/latest/docs)
- [Terraform Best Practices](https://www.terraform-best-practices.com/)

3. **GitHub Actions Documentation**:
- [GitHub Actions Workflows](https://docs.github.com/en/actions/using-workflows)
- [GitHub Actions Security](https://docs.github.com/en/actions/security-guides/security-hardening-for-github-actions)

## 🎉 Conclusion

This guide provides a comprehensive approach to DevOps automation. Remember to:
- Follow security best practices
- Monitor your infrastructure
- Keep dependencies updated
- Document changes and configurations
- Regularly review and update your automation scripts

