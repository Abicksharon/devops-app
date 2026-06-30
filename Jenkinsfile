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

               
stage('Deploy Using Helm') {
    steps {
        sh '''
        export KUBECONFIG=/var/lib/jenkins/.kube/config

        helm upgrade --install devops-app ./helm \
          --set image.repository=abicksharon/devops-app \
          --set image.tag=${BUILD_NUMBER}
        '''
    }
}

}
}
