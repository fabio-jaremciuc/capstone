pipeline {
  agent any
     stages {
         stage('Build Docker Image') {
              steps {
                  sh 'docker build -t capstone-project .'
              }
         }
         stage('Push Docker Image') {
              steps {
                  withDockerRegistry([url: "", credentialsId: "dockerhub"]) {
                      sh 'docker tag capstone-project fabioj/capstone-project:latest'
                      sh 'docker push fabioj/capstone-project:latest'
                  }
              }
         }
       stage('Creates eks cluster') {
              steps{
                  echo 'Creating eks cluster...'
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
