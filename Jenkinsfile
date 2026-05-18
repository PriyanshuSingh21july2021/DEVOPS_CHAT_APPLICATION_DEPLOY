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

        stage('List Files (DEBUG)') {
            steps {
                sh 'ls -R'
            }
        }

        stage('Build Backend') {
            steps {
                sh 'docker build -t $BACKEND_IMAGE ./server'
            }
        }

        stage('Build Frontend') {
            steps {
                sh 'docker build -t $FRONTEND_IMAGE ./frontend || echo "Frontend path missing"'
            }
        }

        stage('Deploy') {
            steps {
                sh 'docker compose down || true'
                sh 'docker compose up -d --build'
            }
        }
    }
}
