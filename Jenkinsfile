pipeline {
    agent any
        stages {
            stage('Deploy') {
                steps {
                    echo 'Deploying...'
                    sh 'eksctl create cluster --name capstone --version 1.17'
                    sh 'kubectl get all'
                }
			}
		}
  environment {
    registry = 'fabioj/capstone'
    registryCredential = 'dockerhub'
    dockerImage = ''
  }
}