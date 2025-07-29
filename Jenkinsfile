pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/vallakkivasisht/k3s-autodeploy.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t my-k3s-app:latest .'
            }
        }

        stage('Load Image to K3s') {
            steps {
                sh 'k3s ctr images import <(docker save my-k3s-app:latest)'
            }
        }

        stage('Deploy to K3s') {
            steps {
                sh 'kubectl apply -f k8s-autodeployment.yaml'
            }
        }
    }
}

