# 🚀 DevOps End-to-End Automation Assignment

Welcome to your first real-world DevOps project! This assignment will help you learn how to build, automate, and deploy a complete web application using modern DevOps tools and AWS infrastructure.

---

## 📌 Objective

Build and deploy a simple Node.js web app using the following DevOps tools and practices:

- Git & GitHub for version control
- Jenkins for CI/CD
- Terraform or CloudFormation for infrastructure
- EC2 on AWS for deployment
- Ansible or shell scripts for server provisioning

---

## 🧱 Folder Structure

```
project/
├── node-app/              # Your Node.js web app
│   ├── server.js
│   ├── package.json
├── infra/                 # Terraform or CloudFormation
│   ├── main.tf / template.yaml
├── ansible/ or scripts/   # Setup automation
│   ├── deploy.yml or setup.sh
├── Jenkinsfile            # CI/CD pipeline (optional)
└── README.md              # This file
```

---

## ✅ Deliverables

- [ ] A working Node.js app pushed to GitHub
- [ ] Jenkins job that installs dependencies and builds the app
- [ ] Terraform or CloudFormation setup to launch an EC2 instance
- [ ] Script or playbook to configure the server and deploy the app
- [ ] Application accessible via public IP on port 3000
- [ ] This `README.md` updated with:
  - Your commands
  - Notes on issues you faced
  - Screenshots (optional)

---

## 🔧 Setup & Commands

### Step 1: Node App

```bash
npm init -y
npm install express
node server.js
```

### Step 2: GitHub Setup

```bash
git init
git remote add origin <repo-url>
git add .
git commit -m "Initial commit"
git push -u origin main
```

### Step 3: EC2 Provisioning

Use Terraform or CloudFormation to provision:
- A t2.micro Ubuntu instance
- Security group with port 22 and 3000 open

### Step 4: Server Setup

```bash
sudo apt update
sudo apt install nodejs npm git -y
git clone <your-repo>
cd node-app
npm install
node server.js
```

Or automate above using a shell script or Ansible playbook.

### Step 5: CI/CD with Jenkins

- Install Jenkins on a server
- Create a Freestyle or Pipeline job
- Connect GitHub repo
- Add build steps: `npm install`, `npm test` (optional)

---

## 🌐 App Test

Visit: `http://<your-ec2-ip>:3000`  
Or run: `curl http://<your-ec2-ip>:3000`

---

## 📸 Screenshots (Optional)

- Jenkins Job
- Terraform apply
- App output in browser

---

## 📚 References

- [Express.js Hello World](https://expressjs.com/en/starter/hello-world.html)
- [Terraform EC2 Example](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/instance)
- [Jenkins Pipeline](https://www.jenkins.io/doc/book/pipeline/)
- [Ansible EC2 Setup](https://www.digitalocean.com/community/tutorials/how-to-use-ansible-to-automate-initial-server-setup-on-ubuntu)

---

## 🙌 Final Tips

- Commit often and push your work regularly.
- Don’t hesitate to document everything.
- If it breaks — that's part of the learning process!

Good luck 💪
