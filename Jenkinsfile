pipeline {
    agent any
        stages {
            stage('Setup Environment') {
                steps {
                    echo 'Setting Up Environment...'
                    
                }
            }
            stage('Deploy') {
                steps {
                    echo 'Deploying...'
                    sh 'eksctl create cluster --name capstone --version 1.17'
                    sh 'kubectl get all'
                }
            }
        }
        environment {
            registry = 'twi5tyx/capstone'
            registryCredential = 'dockerhub'
            dockerImage = ''
        }
}