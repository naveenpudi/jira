pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/naveenpudi/jira.git'
            }
        }

        stage('Prepare Env') {
            steps {
                sh '''
                    echo "Listing project files:"
                    ls -la

                    if [ -f Dockerfile ]; then
                        echo "Found Dockerfile:"
                        cat Dockerfile
                    else
                        echo "⚠️ No Dockerfile found in project root"
                    fi
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
            sh 'docker compose down || true'
        }
    }
}

