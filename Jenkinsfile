pipeline {
    agent any

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'main',
                url: 'https://github.com/sahilmor16/cicd-website.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t cicd-website .'
            }
        }

        stage('Stop Old Container') {
            steps {
                bat '''
                docker stop cicd-container || true
                docker rm cicd-container || true
                '''
            }
        }

        stage('Run Docker Container') {
            steps {
                bat 'docker run -d -p 8081:80 --name cicd-container cicd-website'
            }
        }
    }
}
