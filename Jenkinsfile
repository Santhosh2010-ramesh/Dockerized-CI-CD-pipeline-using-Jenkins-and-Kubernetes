pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'myapp:latest'
        DOCKER_REGISTRY = 'docker.io'
        IMAGE_NAME = 'santhosh2010/myapp'
    }
    stages {
        stage('Clone Code') {
            steps {
                git url:'https://github.com/Santhosh2010-ramesh/Dockerized-CI-CD-pipeline-using-Jenkins-and-Kubernetes.git',branch:'main' // Replace with your repo URL
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t ${DOCKER_IMAGE} .'
                }
            }
        }
        stage('Push to Docker Hub') {
            steps {
                script {
                    withDockerRegistry([credentialsId: 'docker-hub-cred', url: '']) {
                        sh 'docker tag ${DOCKER_IMAGE} ${IMAGE_NAME}'
                        sh 'docker push ${IMAGE_NAME}'
                    }
                }
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                script {
                    sh 'kubectl apply -f k8s-deployment.yaml'  // Your Kubernetes deployment file
                }
            }
        }
    }
}
