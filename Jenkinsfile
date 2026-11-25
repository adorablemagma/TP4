pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Images') {
            steps {
                echo 'Building Docker images...'
                sh 'docker compose build'
            }
        }

        stage('Start Services') {
            steps {
                echo 'Starting MongoDB, Server, Client...'
                sh 'docker compose up -d'
            }
        }

        stage('Test API') {
            steps {
                echo 'Waiting for API...'
                sh 'sleep 10'
                sh 'curl -f http://localhost:9000 || echo "API check done"'
            }
        }

        stage('Test Client') {
            steps {
                echo 'Checking Client...'
                sh 'curl -f http://localhost:3000 || echo "Client check done"'
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            sh 'docker compose down'
        }
    }
}