pipeline {
    agent any

    stages {
        stage('Build Images') {
            steps {
                echo 'Building Docker images...'
                bat 'docker compose build'
            }
        }

        stage('Start Services') {
            steps {
                echo 'Starting MongoDB, Server, Client...'
                bat 'docker compose up -d'
            }
        }

        stage('Test API') {
            steps {
                echo 'Waiting for API...'
                bat 'timeout /t 10 /nobreak > NUL'
                bat 'curl -f http://localhost:9000'
            }
        }

        stage('Test Client') {
            steps {
                echo 'Checking Client...'
                bat 'curl -f http://localhost:3000'
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            bat 'docker compose down'
        }
    }
}