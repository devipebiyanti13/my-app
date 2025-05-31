pipeline {
    agent any

    environment {
        IMAGE_NAME = "flask-app:latest"
    }

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/devipebiyanti13/my-app.git' // ganti dengan URL git milikmu
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t $IMAGE_NAME ."
            }
        }

        stage('Load Image to Minikube') {
            steps {
                sh "minikube image load $IMAGE_NAME"
            }
        }

        stage('Deploy with Helm') {
            steps {
                sh "helm upgrade --install flask-app ./flask-chart" // ganti jadi ./helm kalau foldermu pakai nama 'helm'
            }
        }
    }
}
