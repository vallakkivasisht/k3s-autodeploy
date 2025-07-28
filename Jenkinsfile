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

        stage('Build Docker Image & Load to K3s') {
            steps {
                script {
                    sh "docker build -t ${IMAGE_NAME} ."
                    sh "docker save ${IMAGE_NAME} -o image.tar"
                    sh "sudo k3s ctr images import image.tar"
                }
            }
        }

        stage('Deploy to K3s') {
            steps {
                script {
                    sh "kubectl apply -f deployment.yaml"
                    sh "kubectl rollout restart deployment flask-deployment"
                }
            }
        }
    }
}

