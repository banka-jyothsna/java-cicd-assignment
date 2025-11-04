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
                bat 'mvn clean package'
            }
        }

        stage('Security Scan') {
            steps {
                bat 'echo Running Gitleaks...'
                bat 'echo Running SonarQube analysis...'
                bat 'echo Running Trivy scan...'
            }
        }

        stage('Docker Build & Deploy') {
            steps {
                bat 'echo Building Docker image...'
                bat 'echo Pushing image to Docker Hub...'
                bat 'echo Deploying using Docker Compose...'
            }
        }
    }
}
