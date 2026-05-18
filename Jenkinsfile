pipeline {
    agent any

    environment {
        BACKEND_IMAGE = "chat-backend"
        FRONTEND_IMAGE = "chat-frontend"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/PriyanshuSingh21july2021/DEVOPS_CHAT_APPLICATION_DEPLOY.git'
            }
        }

        stage('Build Backend') {
            steps {
                sh 'docker build -t $BACKEND_IMAGE ./server'
            }
        }

        stage('Build Frontend') {
            steps {
                sh 'docker build -t $FRONTEND_IMAGE ./client'
            }
        }

        stage('Run Containers') {
            steps {
                sh 'docker compose down || true'
                sh 'docker compose up -d --build'
            }
        }
    }
}
