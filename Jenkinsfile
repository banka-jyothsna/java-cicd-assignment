pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Security Scan') {
            steps {
                sh 'echo "Running Gitleaks..."'
                sh 'echo "Running SonarQube analysis..."'
                sh 'echo "Running Trivy scan..."'
            }
        }
        stage('Docker Build & Deploy') {
            steps {
                sh 'echo "Building Docker image..."'
                sh 'echo "Pushing image to Docker Hub..."'
                sh 'echo "Deploying using Docker Compose..."'
            }
        }
    }
}
