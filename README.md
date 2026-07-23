# 🚀 Node.js Application Deployment with GitHub Actions & AWS EC2

This project demonstrates a complete CI/CD pipeline for deploying a Node.js application to an AWS EC2 instance using GitHub Actions and SSH.

## 📌 Features

- Node.js + Express application
- Automated deployment using GitHub Actions
- SSH-based deployment to AWS EC2
- Automatic code pull from GitHub
- Production dependency installation
- Simple REST API

## 🛠️ Tech Stack

- Node.js
- Express.js
- Git & GitHub
- GitHub Actions
- AWS EC2 (Ubuntu)
- SSH

 
## 📁 Project Structure
.
├── .github/
│   └── workflows/
│       └── main.yml
├── index.js
├── package.json
├── package-lock.json
├── Dockerfile
└── README.md
```


## ⚙️ Installation

Clone the repository

```bash
git clone https://github.com/<your-username>/nodejs-application-demo.git
```

Move into the project

```bash
cd nodejs-application-demo
```

Install dependencies

```bash
npm install
```

Start the application

```bash
npm start
```

The server will start on

```
http://localhost:8080
```


## ☁️ AWS EC2 Setup

1. Launch an Ubuntu EC2 instance.
2. Allow inbound traffic on:
   - Port **22** (SSH)
   - Port **8080** (Application)
3. Install Node.js and Git.
4. Clone the repository.
5. Add the GitHub public SSH key to:

```bash
~/.ssh/authorized_keys
```

## 🔑 GitHub Secrets

Go to:

```
Repository
→ Settings
→ Secrets and variables
→ Actions
```

Add the following secret:

| Secret Name | Description |
|-------------|-------------|
| `SSH_KEY` | Private SSH Key used for deployment |


## 🚀 GitHub Actions Workflow

The workflow automatically runs on every push to the `main` branch.

Example:

```yaml
name: Deploy Nodejs Application

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - uses: appleboy/ssh-action@master
        with:
          host: YOUR_EC2_PUBLIC_IP
          username: root
          key: ${{ secrets.SSH_KEY }}
          script: |
            cd /root/nodejs-application-demo
            git pull origin main
            npm install --omit=dev
            pkill node || true
            nohup npm start > app.log 2>&1 &
```

---

## 📡 API

### GET /

Returns

```json
"Hello Everyone!"
```

---

## ▶️ Running Locally

```bash
npm install
npm start
```

Open

```
http://localhost:8080
```

---

## 🔄 CI/CD Flow

```
Developer
      │
      ▼
Git Push
      │
      ▼
GitHub Repository
      │
      ▼
GitHub Actions
      │
      ▼
SSH into EC2
      │
      ▼
Git Pull
      │
      ▼
Install Packages
      │
      ▼
Restart Node.js Server
      │
      ▼
Application Updated




## 👨‍💻 Author

**Ayush Mankar**

GitHub: https://github.com/deadl0x8
