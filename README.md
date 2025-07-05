# 🚀 CI/CD Pipeline for Static Website using Jenkins & Docker

This project showcases a complete CI/CD pipeline that builds and deploys a simple static website using **Jenkins** and **Docker** on an **AWS EC2 instance**.

---

📁 Project Structure
Devops-projects/
├── index.html       # Simple static webpage
├── Dockerfile       # Defines how to build the Docker image
├── Jenkinsfile      # Jenkins Pipeline script for CI/CD
└── README.md        # Project documentation (you're here 🚀)


---

## ⚙️ Technologies Used

- **Jenkins** (Pipeline as Code)
- **Docker**
- **Git & GitHub**
- **AWS EC2 (Ubuntu)**
- **Shell scripting**

---

## 🛠️ Jenkins Pipeline Stages

1. **Clone Repository**
    - Pulls the latest code from GitHub

2. **Build Docker Image**
    - Builds a Docker image with the static website

3. **Stop Old Container**
    - Removes the previous running container (if any)

4. **Run New Container**
    - Starts a new Docker container with the latest image

---

## 🧪 Prerequisites

- Jenkins and Docker installed on an EC2 instance
- Jenkins plugins:
  - **Docker Pipeline**
  - **Blue Ocean**
  - **Git**
- GitHub repository with:
  - `index.html`
  - `Dockerfile`
  - `Jenkinsfile`

---

## 🐳 Dockerfile

```dockerfile
FROM nginx:alpine
COPY index.html /usr/share/nginx/html/index.html
```



## 📄 Jenkinsfile

```groovy
pipeline {
    agent any

    environment {
        IMAGE_NAME = 'my-static-site'
        CONTAINER_NAME = 'static-site-container'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/Hrishikesh2901/simple-docker-website.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("${IMAGE_NAME}")
                }
            }
        }

        stage('Stop Old Container') {
            steps {
                script {
                    sh "docker rm -f ${CONTAINER_NAME} || true"
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    sh "docker run -d --name ${CONTAINER_NAME} -p 80:80 ${IMAGE_NAME}"
                }
            }
        }
    }
}
```


## ✅ Result

After every build, Jenkins automatically:

- Pulls the latest code
- Builds a new Docker image
- Stops the old container
- Runs the updated container on port 80

## ✍️ Author

**Hrishikesh Kamalakar Patil**  
🌐 GitHub: [Hrishikesh2901](https://github.com/Hrishikesh2901)  
🔗 LinkedIn: [linkedin.com/in/hrishikesh-patil-6790b5232](https://www.linkedin.com/in/hrishikesh-patil-6790b5232)
