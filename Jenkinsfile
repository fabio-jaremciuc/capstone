pipeline {
  agent any
     stages {
         stage('Build Docker Image') {
              steps {
                  sh 'docker build -t capstone-project-2 .'
              }
         }
         stage('Push Docker Image') {
              steps {
                  withDockerRegistry([url: "", credentialsId: "dockerhub"]) {
                      sh 'docker tag fabioj/capstone-project-2:latest'
                      sh 'docker push fabioj/capstone-project-2:latest'
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
