pipeline {
    agent any

    environment {
        IMAGE_NAME = "cicd-website"
        CONTAINER_NAME = "cicd-container"
        PORT = "8081"
    }

    stages {
        stage('Checkout Code') {
            steps {
                echo "Cloning repository..."
                git branch: 'main', url: 'https://github.com/sahilmor16/cicd-website.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo "Building Docker image..."
                bat """
                docker build -t %IMAGE_NAME% .
                """
            }
        }

        stage('Stop Old Container') {
            steps {
                echo "Stopping old container if exists..."
                bat """
                @echo off
                docker stop %CONTAINER_NAME% 2>NUL || echo Container not running
                docker rm %CONTAINER_NAME% 2>NUL || echo Container not exists
                """
            }
        }

        stage('Run Docker Container') {
            steps {
                echo "Running new Docker container..."
                bat """
                docker run -d -p %PORT%:80 --name %CONTAINER_NAME% %IMAGE_NAME%
                """
            }
        }
    }

    post {
        success {
            echo "Pipeline finished successfully! 🎉"
        }
        failure {
            echo "Pipeline failed. ❌ Check logs for details."
        }
    }
}
