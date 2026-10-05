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
                bat 'docker build -t devops-static-website .'
            }
        }

        stage('Stop Old Container') {
            steps {
                bat 'docker stop devops-static-website-container || exit 0'
                bat 'docker rm devops-static-website-container || exit 0'
            }
        }

        stage('Run Docker Container') {
            steps {
                bat 'docker run -d -p 8080:80 --name devops-static-website-container devops-static-website'
            }
        }

        stage('Verify Website') {
            steps {
                bat 'curl http://localhost:8080'
            }
        }
    }
}