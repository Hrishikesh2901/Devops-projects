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
