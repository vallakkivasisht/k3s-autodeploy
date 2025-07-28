pipeline {
    agent any

    environment {
        IMAGE_NAME = 'flask-k3s-app:latest'
    }

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/vallakkivasisht/k3s-autodeploy.git'
            }
        }

        stage('Build Docker Image Locally') {
            steps {
                script {
                    sh "docker build -t ${IMAGE_NAME} ."
                }
            }
        }

        stage('Deploy to K3s with Local Image') {
            steps {
                script {
                    sh "kubectl apply -f deployment.yaml"
                    sh "kubectl rollout restart deployment flask-deployment"
                }
            }
        }
    }
}

