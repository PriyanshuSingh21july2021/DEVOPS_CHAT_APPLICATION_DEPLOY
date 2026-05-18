pipeline {
    agent any

    environment {
        BACKEND_IMAGE = "chat-backend"
        FRONTEND_IMAGE = "chat-frontend"
    }

    stages {

        stage('Cleanup Old Containers') {
            steps {
                sh '''
                    docker compose down -v || true
                    docker rm -f $(docker ps -aq) || true
                    docker system prune -f || true
                '''
            }
        }

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                url: 'https://github.com/PriyanshuSingh21july2021/DEVOPS_CHAT_APPLICATION_DEPLOY.git'
            }
        }

        stage('Build Backend Image') {
            steps {
                sh 'docker build -t $BACKEND_IMAGE ./server'
            }
        }

        stage('Build Frontend Image') {
            steps {
                sh 'docker build -t $FRONTEND_IMAGE ./public'
            }
        }

        stage('Deploy with Docker Compose') {
            steps {
                sh 'docker compose up -d --build'
            }
        }

        stage('Verify Deployment') {
            steps {
                sh '''
                    sleep 10
                    curl -f http://localhost:5000/ping || exit 1
                '''
            }
        }
    }

    post {
        success {
            echo "✅ Pipeline SUCCESS - App deployed"
        }
        failure {
            echo "❌ Pipeline FAILED - check logs"
        }
    }
}
