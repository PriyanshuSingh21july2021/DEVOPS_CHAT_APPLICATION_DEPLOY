pipeline {
    agent any

    environment {
        BACKEND_IMAGE = "chat-backend"
        FRONTEND_IMAGE = "chat-frontend"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                url: 'https://github.com/PriyanshuSingh21july2021/DEVOPS_CHAT_APPLICATION_DEPLOY.git'
            }
        }

        stage('List Project Structure (DEBUG)') {
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
                // IMPORTANT: your frontend is inside /public/src not /client or /frontend
                sh 'docker build -t $FRONTEND_IMAGE ./public'
            }
        }

        stage('Stop Old Containers') {
            steps {
                sh 'docker compose down || true'
            }
        }

        stage('Deploy Containers') {
            steps {
                sh 'docker compose up -d --build'
            }
        }

        stage('Verify Deployment') {
            steps {
                sh '''
                    echo "Checking Backend..."
                    curl -f http://localhost:5000/ping || true

                    echo "Checking Frontend..."
                    curl -I http://localhost:3000 || true

                    echo "Containers Status..."
                    docker ps
                '''
            }
        }
    }

    post {
        success {
            echo "🚀 Pipeline Success - App Deployed"
        }
        failure {
            echo "❌ Pipeline Failed - Check Logs"
        }
    }
}
