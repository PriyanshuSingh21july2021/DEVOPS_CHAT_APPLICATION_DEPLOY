pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                url: 'https://github.com/PriyanshuSingh21july2021/DEVOPS_CHAT_APPLICATION_DEPLOY.git'
            }
        }

        stage('Clean Old Containers') {
            steps {
                sh '''
                    docker compose down || true
                    docker rm -f $(docker ps -aq) || true
                '''
            }
        }

        stage('Build Backend') {
            steps {
                sh 'docker build -t chat-backend ./server'
            }
        }

        stage('Build Frontend') {
            steps {
                sh 'docker build -t chat-frontend ./public'
            }
        }

        stage('Deploy') {
            steps {
                sh 'docker compose up -d --build'
            }
        }

        stage('Verify') {
            steps {
                sh '''
                    curl -f http://localhost:5000/ping || true
                    curl -I http://localhost:3000 || true
                    docker ps
                '''
            }
        }
    }

    post {
        success {
            echo "DEPLOY SUCCESS"
        }
        failure {
            echo "DEPLOY FAILED - CHECK PORTS"
        }
    }
}
