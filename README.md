# 🚀 DevOps CI/CD Automation Project

This project demonstrates **how I built a complete CI/CD pipeline from scratch**, starting with a simple Python app and culminating in a **live, deployed application** using GitHub, Jenkins, Docker, and AWS.

I built an end-to-end CI/CD pipeline using GitHub Actions for CI and Jenkins for CD. The application is Dockerized and deployed automatically on a Linux server. 
I also handled issues like Docker permissions, Jenkins workspace corruption, Docker cache problems, and AWS security configuration.

This README explains **everything step by step**.

---

# 📌 1. What is this project?

This is an **end-to-end DevOps CI/CD automation project**.

What it does:
- Takes source code from GitHub
- Automatically tests it
- Automatically builds a Docker image
- Automatically deploys the app on a Linux server
- Updates the live website when code changes

👉 **No manual deployment**

---

# 🎯 2. Why this project?

In real companies:
- Manual deployment causes errors
- Developers should not SSH and deploy manually
- CI/CD automates everything

This project solves that by using:
- **CI (Continuous Integration)** → GitHub Actions
- **CD (Continuous Deployment)** → Jenkins
- **Docker** → consistent runtime
- **AWS EC2** → real cloud server

---

# 🛠️ 3. Tools Used

| Purpose     | Tool |
|-------------|------|
| Source Code | GitHub |
| CI          | GitHub Actions |
| CD          | Jenkins |
| Container   | Docker |
| OS          | Linux (Ubuntu) |
| Cloud       | AWS EC2 |
| Language    | Python |
| Framework   | Flask |
| Testing     | Pytest |

---

# 🏗️ 4. How this project works (Flow)

```
Code Change
   ↓
git push to GitHub
   ↓
GitHub Actions runs tests (CI)
   ↓
Jenkins runs deployment (CD)
   ↓
Docker builds new image
   ↓
Old container removed
   ↓
New container deployed
   ↓
Website updated automatically
```
---

# 🧪 5. CI – GitHub Actions 

CI runs **automatically** when code is pushed.

Steps:
1. Checkout code
2. Setup Python
3. Install dependencies
4. Install pytest
5. Run tests

If tests fail → deployment stops.

---

# 🚀 6. CD – Jenkins (What happens)

Jenkins does the deployment.

Steps:
1. Clone GitHub repository
2. Build Docker image
3. Stop old container
4. Run new container

Commands used:
```bash
docker stop cicd-app || true
docker rm cicd-app || true
docker build --no-cache -t cicd-app:latest .
docker run -d -p 5000:5000 --name cicd-app cicd-app:latest
```

---

# 🐳 7. Docker Explanation

- App is packed inside a Docker image
- Same image runs everywhere
- No dependency issues

Dockerfile builds the image and exposes port `5000`.

---

# ☁️ 8. AWS Setup

- Ubuntu EC2 instance created
- Jenkins runs inside Docker on EC2
- Security Group allows:
  - SSH (22)
  - Jenkins (8080)
  - App (5000)

Inbound rule added:
```
Custom TCP | Port 5000 | 0.0.0.0/0
```

---

# ⚠️ 9. Problems I Faced & Fixed

| Problem                  | Fix |
|--------------------------|----|
| pytest not found         | Installed pytest |
| docker not found         | Installed Docker CLI in Jenkins |
| permission denied        | Ran Jenkins as root |
| Jenkins workspace broken | Deleted workspace |
| code not updating        | Disabled Docker cache |
| site not opening         | Fixed AWS security group |

---

# ▶️ 10. How to clone and run this project locally

```bash
git clone https://github.com/Akash642-eng/devops-cicd-automation.git
cd devops-cicd-automation
docker build -t cicd-app .
docker run -p 5000:5000 cicd-app
```

Open:
```
http://localhost:5000
```

---

# 🔁 11. How to update the live website

1. Change code in `app.py`
2. Run:
```bash
git add .
git commit -m "Update message"
git push origin main
```

3. CI/CD runs automatically
4. Website updates automatically

---

# 🌍 12. Live Application

```
http://<EC2-PUBLIC-IP>:5000
```

---
Python & DevOps Enthusiast  
GitHub: https://github.com/Akash642-eng
