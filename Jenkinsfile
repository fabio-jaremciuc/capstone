pipeline {
  agent any
     stages {
         stage('Lint') {
              steps {
                  sh 'hadolint Dockerfile'
              }
          }
         stage('Build Docker Image') {
              steps {
                  sh "docker build -t fabioj/capstone-project:${env.BUILD_NUMBER} ."
              }
         }
         stage('Push Docker Image') {
              steps {
                  withDockerRegistry([url: "", credentialsId: "dockerhub"]) {
                      sh "docker push fabioj/capstone-project:${env.BUILD_NUMBER}"
                  }
              }
         }
       stage('Creates eks cluster') {
              steps{
                  withAWS(credentials: 'demo-ecr-credentials', region: 'us-east-2') {
                      sh 'eksctl create cluster --region us-east-2 --name capstone-project --nodes-min 2 --nodes-max 2 --node-type t2.micro'
                      echo 'Cluster created!'
                  }
              }
        }
        stage('Deploying') {
              steps{
                  echo 'Deploying to AWS...'
                  withAWS(credentials: 'demo-ecr-credentials', region: 'us-east-2') {
                      sh 'aws eks --region us-east-2 update-kubeconfig --name capstone-project'
                      sh 'kubectl apply -f deployment.yml'
                      sh 'kubectl get all'
                  }
              }
        }
        stage("Cleaning up") {
              steps{
                    echo 'Cleaning up...'
                    sh 'docker system prune'
              }
        }
     }
}
