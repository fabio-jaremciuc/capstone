pipeline {
  agent any
     stages {
         stage('Setup Environment') {
              steps {
                    echo 'Setting Up Environment...'
                    sh "make setup"
                    sh 'make install'
              }
         }
         stage('Lint') {
              steps {
                    echo 'Linting...'
                    sh "make lint"
              }
         }
         stage('Build Docker Image') {
              steps {
                  sh 'docker build -t capstone .'
              }
         }
         stage('Push Docker Image') {
              steps {
                  withDockerRegistry([url: "", credentialsId: "dockerhub"]) {
                      sh 'docker tag fabioj/capstone-project-1'
                      sh 'docker push fabioj/capstone-project-1'
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
