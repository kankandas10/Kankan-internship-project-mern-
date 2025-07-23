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

        // Optional: Add test or lint stage here
        // stage('Run Tests') {
        //     steps {
        //         sh 'docker exec backend npm test'
        //     }
        // }

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




