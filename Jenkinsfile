pipeline {
    agent any

    environment {
        IMAGE_NAME = "devipebiyanti/flask-app:latest"
    }

    stages {
        stage('Build Docker Image') {
            steps {
                sh "docker build -t $IMAGE_NAME ."
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials-id', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                    sh "docker push $IMAGE_NAME"
                }
            }
        }

        stage('Deploy with Helm') {
            steps {
                sh "helm upgrade --install flask-app ./flask-chart --set image.repository=devipebiyanti/flask-app --set image.tag=latest"
            }
        }
    }
}
