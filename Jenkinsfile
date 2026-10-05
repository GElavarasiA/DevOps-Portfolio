pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t devops-static-website .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh 'docker rm -f devops-static-website-container || true'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh 'docker run -d -p 8082:80 --name devops-static-website-container devops-static-website'
            }
        }

        stage('Verify Container') {
            steps {
                sh 'docker ps --filter name=devops-static-website-container'
            }
        }
    }
}