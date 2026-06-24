pipeline {
    agent any

    stages {

        stage('Build Docker Image') {
            steps {
                sh '''
                docker build -t devops-app:${BUILD_NUMBER} .
                '''
            }
        }

        stage('Push To Docker Hub') {
            steps {
                sh '''
                docker tag devops-app:${BUILD_NUMBER} abicksharon/devops-app:${BUILD_NUMBER}
                docker push abicksharon/devops-app:${BUILD_NUMBER}
                '''
            }
        }

        stage('Deploy To Kubernetes') {
            steps {
                sh '''
                export KUBECONFIG=/var/lib/jenkins/.kube/config

                kubectl set image deployment/devops-app \
                devops-app=abicksharon/devops-app:${BUILD_NUMBER}
                '''
            }
        }
    }
}
