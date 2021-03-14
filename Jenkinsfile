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
        stage("Cleaning up") {
              steps{
                    echo 'Cleaning up...'
                    sh "docker system prune"
              }
        }
     }
}
