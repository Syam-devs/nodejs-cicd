# 🚀 End-to-End CI/CD Pipeline Using Jenkins, Docker, GitHub & Docker Hub

## 📖 Project Overview

This project demonstrates a complete **CI/CD pipeline** using
**Jenkins**, **Docker**, **GitHub**, and **Docker Hub** on an Ubuntu
machine.

Whenever code is pushed to GitHub, Jenkins automatically:

-   Checks out the latest source code
-   Builds a Docker image
-   Pushes the image to Docker Hub
-   Pulls the latest image
-   Deploys the latest container

------------------------------------------------------------------------

# 🏗️ Architecture

``` text
Developer
    |
    v
GitHub Repository
    |
    v
Jenkins Pipeline
    |
    +--> Checkout Code
    |
    +--> Build Docker Image
    |
    +--> Docker Login
    |
    +--> Push Image
    |
    +--> Pull Latest Image
    |
    +--> Deploy Container
    |
    v
Node.js Application
```

------------------------------------------------------------------------

# 🛠️ Tech Stack

-   Ubuntu 22.04 LTS
-   Java 17
-   Jenkins
-   Docker
-   Git
-   GitHub
-   Docker Hub
-   Node.js

------------------------------------------------------------------------

# 📋 Prerequisites

-   Ubuntu 22.04 LTS
-   4 GB RAM (8 GB Recommended)
-   Docker Hub Account
-   GitHub Account
-   Internet Connection

------------------------------------------------------------------------

# Step 1 - Install Java

``` bash
sudo apt update
sudo apt install openjdk-17-jdk -y
java -version
```

------------------------------------------------------------------------

# Step 2 - Install Jenkins

Add the Jenkins key.

``` bash
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null
```

Add the Jenkins repository.

``` bash
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
```

Install Jenkins.

``` bash
sudo apt update
sudo apt install jenkins -y
sudo systemctl enable jenkins
sudo systemctl start jenkins
sudo systemctl status jenkins
```

Get the initial admin password.

``` bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

Open Jenkins:

``` text
http://localhost:8080
```

Install the suggested plugins.

------------------------------------------------------------------------

# Step 3 - Install Docker

``` bash
sudo apt install docker.io -y
sudo systemctl enable docker
sudo systemctl start docker
docker --version
```

------------------------------------------------------------------------

# Step 4 - Configure Jenkins to Use Docker

``` bash
sudo usermod -aG docker jenkins
sudo systemctl restart docker
sudo systemctl restart jenkins
groups jenkins
```

Expected output:

``` text
jenkins docker
```

------------------------------------------------------------------------

# Step 5 - Install Git

``` bash
sudo apt install git -y
git --version
```

------------------------------------------------------------------------

# Step 6 - Create Docker Hub Repository

Create a repository named:

``` text
nodejs-cicd
```

------------------------------------------------------------------------

# Step 7 - Create Node.js Application

Create project.

``` bash
mkdir nodejs-cicd
cd nodejs-cicd
```

Create **app.js**

``` javascript
const express = require('express');

const app = express();

app.get('/', (req,res)=>{
    res.send("DevOps CI/CD Project Working");
});

app.listen(3000,()=>{
    console.log("Running on Port 3000");
});
```

Create **package.json**

``` json
{
  "name":"nodejs-cicd",
  "version":"1.0.0",
  "scripts":{
    "start":"node app.js",
    "test":"echo Test Passed"
  },
  "dependencies":{
    "express":"^5.1.0"
  }
}
```

Install dependencies.

``` bash
npm install
```

------------------------------------------------------------------------

# Step 8 - Create Dockerfile

``` dockerfile
FROM node:20-alpine

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 3000

CMD ["npm","start"]
```

Test locally.

``` bash
docker build -t nodejs-cicd .
docker run -d -p 3000:3000 nodejs-cicd
```

------------------------------------------------------------------------

# Step 9 - Push Code to GitHub

``` bash
git init
git add .
git commit -m "Initial Commit"
git branch -M main
git remote add origin YOUR_REPOSITORY_URL
git push -u origin main
```

------------------------------------------------------------------------

# Step 10 - Install Jenkins Plugins

Install:

-   Pipeline
-   Git
-   Git Client
-   Docker Pipeline
-   Credentials Binding
-   GitHub

------------------------------------------------------------------------

# Step 11 - Configure Docker Hub Credentials

Navigate to:

``` text
Manage Jenkins
→ Credentials
→ System
→ Global Credentials
```

Create credentials:

``` text
Username : Docker Hub Username
Password : Docker Hub Password / Access Token
ID       : dockerhub
```

------------------------------------------------------------------------

# Step 12 - Create Pipeline Job

``` text
New Item
↓
Pipeline
↓
NodeJS-CICD
```

------------------------------------------------------------------------

# Step 13 - Add Jenkinsfile

Create a `Jenkinsfile` in the project root and paste your pipeline code.

Commit and push:

``` bash
git add .
git commit -m "Added Jenkinsfile"
git push
```

------------------------------------------------------------------------

# Step 14 - Run the Pipeline

Click **Build Now**.

Pipeline Flow:

``` text
Checkout
   ↓
Docker Build
   ↓
Docker Login
   ↓
Docker Push
   ↓
Docker Pull
   ↓
Deploy Container
```

------------------------------------------------------------------------

# Step 15 - Verify Deployment

``` bash
docker ps
docker images
```

Open:

``` text
http://localhost:3000
```

Expected output:

``` text
DevOps CI/CD Project Working
```

------------------------------------------------------------------------

# 📸 Screenshots

Add screenshots for:

-   Jenkins Dashboard
-   Successful Pipeline
-   Docker Hub Repository
-   GitHub Repository
-   Running Container
-   Application Output

------------------------------------------------------------------------

# 🎯 Learning Outcomes

-   CI/CD Fundamentals
-   Jenkins Pipelines
-   Docker
-   GitHub Integration
-   Docker Hub
-   Container Deployment
-   Automation
-   DevOps Workflow
