
# DevOps End-to-End Automation Project Guide

---

## 🎯 Objective

Learn and practice essential DevOps tasks: AWS authentication, infrastructure automation with Terraform, basic Node.js app deployment, and CI/CD automation using GitHub Actions.

---

## ✅ Step 1: Validate AWS CLI and Configure Authentication

### 📌 Pre-requisites Check

Check if AWS CLI is installed:

```bash
aws --version
```

If not installed:

```bash
sudo apt install awscli -y     # Ubuntu
brew install awscli            # Mac
```

Check if AWS credentials are configured:

```bash
aws sts get-caller-identity
```

If you see an error, configure AWS credentials:

```bash
aws configure
```

Verify AWS credentials file:

```bash
cat ~/.aws/credentials
```

---

## ✅ Step 2: Validate Terraform Installation and Setup

Check if Terraform is installed:

```bash
terraform -version
```

If not installed:

```bash
sudo apt install unzip -y
wget https://releases.hashicorp.com/terraform/1.5.0/terraform_1.5.0_linux_amd64.zip
unzip terraform_1.5.0_linux_amd64.zip
sudo mv terraform /usr/local/bin/
terraform -version
```

---

## ✅ Step 3: Provision AWS Resources with Terraform

Create a Terraform project:

```bash
mkdir aws-terraform-demo && cd aws-terraform-demo
```

Sample `main.tf`:

```hcl
provider "aws" {
  region = "us-east-1"
}

resource "aws_s3_bucket" "demo_bucket" {
  bucket = "my-unique-bucket-name-123456"
  acl    = "private"
}

resource "aws_security_group" "web_sg" {
  name        = "allow_web_traffic"
  description = "Allow HTTP and SSH traffic"

  ingress {
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  ingress {
    from_port   = 3000
    to_port     = 3000
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }
}

resource "aws_instance" "demo_instance" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
  security_groups = [aws_security_group.web_sg.name]

  tags = {
    Name = "DemoEC2"
  }
}
```

Execution:

```bash
terraform init
terraform apply
```

---

## ✅ Step 4: Validate Node.js Installation and Build App

Check if Node.js is installed:

```bash
node -v
npm -v
```

If not installed:

```bash
sudo apt install -y nodejs npm   # Ubuntu
brew install node                # Mac
```

Create Node.js App:

```bash
mkdir node-app && cd node-app
npm init -y
npm install express
```

Create `server.js`:

```js
const express = require('express');
const app = express();
const port = 3000;

app.get('/', (req, res) => res.send('Hello from FastCart!'));
app.listen(port, () => console.log(`App running on port ${port}`));
```

Run:

```bash
node server.js
```

Test:  
Visit `http://localhost:3000`

---

## ✅ Step 5: Setup GitHub Actions for CI/CD

Create `.github/workflows/deploy.yml`:

```yaml
name: Deploy Node.js App to EC2

on:
  push:
    branches: [ main ]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v2

      - name: Setup SSH Key
        run: |
          mkdir -p ~/.ssh
          echo "${{ secrets.EC2_SSH_KEY }}" > ~/.ssh/id_rsa
          chmod 600 ~/.ssh/id_rsa

      - name: Deploy to EC2
        run: |
          ssh -o StrictHostKeyChecking=no ubuntu@<EC2-Public-IP> << 'EOF'
            cd ~/node-app
            git pull origin main
            npm install
            pkill node || true
            nohup node server.js &
          EOF
```

---

# 🎉 **End of Guide**

