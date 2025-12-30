pipeline {
    agent any

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'main',
                url: 'https://github.com/<your-username>/cicd-jenkins-docker.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t cicd-website .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh '''
                docker stop cicd-container || true
                docker rm cicd-container || true
                '''
            }
        }

        stage('Run Docker Container') {
            steps {
                sh 'docker run -d -p 8081:80 --name cicd-container cicd-website'
            }
        }
    }
}
