pipeline {
    agent any

    environment {
        DOCKER_HUB_USER = 'your-dockerhub-username'
        DOCKER_HUB_PASS = credentials('dockerhub-credentials-id')
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://your-repo-url.git'
            }
        }

        stage('Build Backend Image') {
            steps {
                sh 'docker build -t backend_app:latest ./backend'
            }
        }

        stage('Build Frontend Image') {
            steps {
                sh 'docker build -t frontend_app:latest ./frontend'
            }
        }

        stage('Compose Up') {
            steps {
                sh 'docker-compose up -d --build'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    sh 'echo $DOCKER_HUB_PASS | docker login -u $DOCKER_HUB_USER --password-stdin'
                    sh 'docker tag backend_app:latest $DOCKER_HUB_USER/backend_app:latest'
                    sh 'docker tag frontend_app:latest $DOCKER_HUB_USER/frontend_app:latest'
                    sh 'docker push $DOCKER_HUB_USER/backend_app:latest'
                    sh 'docker push $DOCKER_HUB_USER/frontend_app:latest'
                }
            }
        }
    }

    post {
        always {
            sh 'docker-compose down'
        }
    }
}
