pipeline {
    agent any

    environment {
        COMPOSE_PROJECT_NAME = "kankan-mern"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/kankandas10/Kankan-internship-project-mern-.git'
            }
        }

        stage('Clean Up Previous Containers') {
            steps {
                // Remove old conflicting containers
                sh '''
                  docker rm -f admin || true
                  docker rm -f frontend || true
                  docker rm -f backend || true
                  docker rm -f mongo || true
                '''
            }
        }

        stage('Build & Run with Docker Compose') {
            steps {
                sh 'docker compose down'
                sh 'docker compose up -d --build'
            }
        }

        stage('Verify Services') {
            steps {
                sh 'docker ps'
            }
        }

        stage('Cleanup Old Images (Optional)') {
            steps {
                sh 'docker image prune -f'
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed.'
        }
    }
}
