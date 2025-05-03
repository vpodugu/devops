# Week 1 DevOps Homework: Deploy and Containerize a Node.js App

Welcome to your first DevOps hands-on project! 🚀

In this assignment, you will set up your first AWS server, deploy a basic Node.js web server, containerize it using Docker, and manage your code using Git and GitHub.

This exercise will solidify your understanding of AWS EC2, Linux basics, web servers, containerization, and version control — foundational skills for any DevOps Engineer!

---

## 🎯 Objective

- Launch an EC2 instance on AWS.
- Deploy a custom Node.js (Express.js) web server.
- Containerize the application using Docker.
- Push all code to a GitHub repository.
- Practice troubleshooting common DevOps setup issues.

---

## 🛠️ Tasks to Complete

1. **Provision an AWS EC2 Instance**  
   - Use Ubuntu 20.04 LTS (Free Tier t2.micro)
   - Open ports 22 (SSH) and 3000 (Node app) in the Security Group.

2. **Install Node.js and Create a Simple Web Server**
   - Install Node.js and npm.
   - Create a small Express.js app returning a basic web page.

3. **Test Your Node.js App**
   - Access your server via `http://<your-ec2-ip>:3000`

4. **Containerize Your App**
   - Write a Dockerfile.
   - Build and run the app inside a Docker container.

5. **Push Your Work to GitHub**
   - Upload `server.js`, `Dockerfile`, `package.json`, and optionally a `README.md`.

---

## 🖥️ Expected Deliverables

- GitHub repository link containing:
  - `server.js`
  - `package.json`
  - `Dockerfile`
  - (Optional) `README.md`
- Live app accessible at: `http://<your-ec2-public-ip>:3000`
- Screenshot of app running (optional but encouraged).

---

## 🔗 Helpful Reading Material

- [AWS EC2 Launch and Connect Guide](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html)
- [AWS Security Groups Basics](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html)
- [Node.js Express Quick Start](https://expressjs.com/en/starter/hello-world.html)
- [Docker Getting Started Guide](https://docs.docker.com/get-started/)
- [GitHub Basic Workflow](https://docs.github.com/en/get-started/quickstart)

---

## ✅ Submission Checklist

- [ ] EC2 instance launched and accessible.
- [ ] Node.js server running successfully.
- [ ] Docker container created and tested.
- [ ] Code pushed to GitHub repository.
- [ ] Shared GitHub repo link with instructor.
- [ ] (Optional) Screenshot of live app attached.

---

## 🚀 Bonus (Optional)

- Create a basic `README.md` for your GitHub repo explaining what you built.
- Try exposing environment variables (e.g., PORT) in your Dockerfile.
- Explore CloudWatch to monitor your EC2 instance metrics.

---

Good luck, and have fun learning DevOps the real way! 💻🔥


