pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://your-repo-url.git'
            }
        }

        stage('Prepare Env') {
            steps {
                sh '''
                cat > backend/.env <<EOL
                DATABASE_URL=postgresql://user:password@db:5432/mydb
                SECRET_KEY=supersecret
                EOL
                '''
            }
        }

        stage('Build and Run with Docker Compose') {
            steps {
                sh 'docker compose up -d --build'
            }
        }
    }

    post {
        always {
            sh 'docker compose down'
        }
    }
}
