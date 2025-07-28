pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('vallakki') // Your Jenkins credentials ID
        IMAGE_NAME = 'vallakki/flask-k3s-app:latest'
    }

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/vallakkivasisht/k3s-autodeploy.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${IMAGE_NAME} ."
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                script {
                    sh "echo ${DOCKERHUB_CREDENTIALS_PSW} | docker login -u ${DOCKERHUB_CREDENTIALS_USR} --password-stdin"
                    sh "docker push ${IMAGE_NAME}"
                }
            }
        }

        stage('Deploy to K3s') {
            steps {
                sh 'kubectl apply -f deployment.yaml'
                sh 'kubectl rollout restart deployment flask-deployment'
            }
        }
    }
}

