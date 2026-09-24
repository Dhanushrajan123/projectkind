pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Docker Build') {
            steps {
                bat 'docker build -t dhanush-app:latest .'
            }
        }

        stage('Load Image to Kind') {
    steps {
        bat 'where kind'
        bat 'kind version'
        bat 'kind load docker-image dhanush-app:latest --name dhanush'
    }
}
        stage('Deploy to Kubernetes') {
            steps {
                bat 'kubectl apply -f deployment.yaml'
                bat 'kubectl apply -f service.yaml'
            }
        }

        stage('Verify Deployment') {
            steps {
                bat 'kubectl get pods'
                bat 'kubectl get deployment'
                bat 'kubectl get service'
            }
        }
    }
}
