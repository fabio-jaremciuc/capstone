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
                  sh "docker build -t fabioj/capstone-project:latest ."
              }
         }
         stage('Push Docker Image') {
              steps {
                  withDockerRegistry([url: "", credentialsId: "dockerhub"]) {
                      sh "docker push fabioj/capstone-project:latest"
                  }
              }
         }
        stage('Deploying') {
              steps{
                  echo 'Deploying to AWS...'
                  withAWS(credentials: 'demo-ecr-credentials', region: 'us-east-2') {
                    sh 'aws eks --region us-east-2 update-kubeconfig --name capstone-project'
                    sh 'kubectl apply -f deployment.yml'
                    sh 'kubectl rollout status deployment/capstone-project'  
                    sh 'kubectl get nodes'
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
