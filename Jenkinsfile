pipeline {
    agent any

    tools {
        jdk 'JDK11'
        maven 'Maven_3'
    }

    environment {
        IMAGE_NAME = "java-cicd-assignment"
        TAG = "latest"
    }

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
                bat 'echo Running Gitleaks... (Secret Scan Simulation)'
                bat 'echo Running SonarQube analysis... (Code Quality Simulation)'
                bat 'echo Running Trivy scan... (Vulnerability Scan Simulation)'
            }
        }

        stage('Docker Build & Deploy') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    bat '''
                    echo Logging in to Docker Hub...
                    docker login -u %DOCKER_USER% -p %DOCKER_PASS%

                    echo Building Docker image...
                    docker build -t %DOCKER_USER%/%IMAGE_NAME%:%TAG% .

                    echo Pushing Docker image to Docker Hub...
                    docker push %DOCKER_USER%/%IMAGE_NAME%:%TAG%

                    echo Deploying application using Docker Compose...
                    docker-compose down
                    docker-compose up -d
                    '''
                }
            }
        }
    }

    post {
        success {
            echo '✅ Build, Scan, and Deployment completed successfully!'
        }
        failure {
            echo '❌ Build failed. Please check the logs for more details.'
        }
    }
}
