pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/naveenpudi/jira.git'
            }
        }

        stage('Build and Run with Docker Compose') {
            steps {
                sh 'docker-compose up -d --build'
            }
        }
    }

    post {
        always {
            sh 'docker-compose down'
        }
    }
}
