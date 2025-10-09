# 🚀 Next.js Docker GHCR Pipeline  

A simple **Next.js starter app** containerized with **Docker** and automated using **GitHub Actions** to build and push Docker images to the **GitHub Container Registry (GHCR)**.  

This project focuses on **DevOps automation workflows**, not app development.  
It demonstrates the end-to-end CI/CD process — from code commit → container image → registry → deployment on Ubuntu (EC2).  

---

## 🧩 Tech Stack

- **Frontend Framework:** Next.js (Basic Starter Template)  
- **Runtime:** Node.js 20  
- **Containerization:** Docker  
- **Automation:** GitHub Actions (CI/CD)  
- **Image Registry:** GitHub Container Registry (GHCR)  
- **OS/Environment:** Ubuntu (EC2 Instance)

---

## 📁 Folder Structure

nextjs-docker-ghcr-pipeline/
│
├── Dockerfile
├── .dockerignore
├── package.json
├── next.config.js
├── pages/
├── public/
└── .github/
└── workflows/
└── docker-build.yml

yaml
Copy code

---

## ⚙️ Project Setup

1️⃣ Clone the Repository

          git clone https://github.com/<your-username>/nextjs-docker-ghcr-pipeline.git
          cd nextjs-docker-ghcr-pipeline
2️⃣ Install Dependencies
         
          npm install
3️⃣ Run Locally
          
          npm run dev
          The app will be accessible at: http://localhost:3000

🐳 Docker Commands
Build Docker Image
          
          docker build -t nextjs-ghcr-app .
Run Container

          docker run -p 3000:3000 nextjs-ghcr-app


🔁 GitHub Actions Workflow (CI/CD)
This workflow automatically:

    Builds the Docker image when code is pushed to main

    Tags the image as latest

    Pushes it to GitHub Container Registry (GHCR)

Workflow File: .github/workflows/docker-build.yml


name: Build and Push Docker Image

on:
  push:
    branches:
      - main

jobs:
  build:
  
    runs-on: ubuntu-latest
    steps:
    
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Log in to GHCR
        uses: docker/login-action@v3
        with:
          registry: ghcr.io
          username: ${{ github.actor }}
          password: ${{ secrets.GITHUB_TOKEN }}

      - name: Build Docker image
        run: |
          docker build -t ghcr.io/${{ github.repository_owner }}/nextjs-ghcr-app:latest .

      - name: Push Docker image
        run: |
          docker push ghcr.io/${{ github.repository_owner }}/nextjs-ghcr-app:latest
🧠 Learning Outcomes
Through this project, I learned how to:

    ✅ Containerize a web app using Docker
    ✅ Create and configure a GitHub Actions CI/CD workflow
    ✅ Push Docker images securely to GHCR
    ✅ Deploy and test containers on Ubuntu EC2
    ✅ Understand the DevOps lifecycle from source → automation → deployment

🔧 Requirements

    Node.js 20+  
    
    Docker installed on local or EC2 machine
    
    GitHub account with Actions enabled
    
    Ubuntu EC2 instance (for testing)

🧱 Pipeline Overview


    Developer Commit
           ↓
    GitHub Repository
           ↓
    GitHub Actions (CI/CD Workflow)
           ↓
    Docker Image Build
           ↓
    Push to GitHub Container Registry (GHCR)
           ↓
    Run Container on Ubuntu EC2


👨‍💻 Author

      Shreyas Deshpande
      Cloud & DevOps Engineer | Docker | GitHub Actions | CI/CD | Cloud Automation
      🔗 LinkedIn
      📦 GitHub

📜 License
          This project is open-source and available under the MIT License.

⭐ If you found this project useful, give it a star on GitHub!



