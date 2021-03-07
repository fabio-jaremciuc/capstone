pipeline {
  agent any
  stages {
    stage('Setup Environment') {
      steps {
        echo 'Setting Up Environment...'
        sh '''make setup
                          make install
                    '''
      }
    }

    stage('Lint') {
      steps {
        echo 'Linting...'
        sh 'make lint'
      }
    }

    stage('Build') {
      steps {
        echo 'Building...'
        script {
          dockerImage = docker.build registry + ":latest"
        }

      }
    }

    stage('Upload') {
      steps {
        echo 'Uploading to DockerHub...'
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }

      }
    }

    stage('Deploy') {
      steps {
        echo 'Deploying...'
        sh 'aws eks --region us-east-2 update-kubeconfig --name capstone'
        sh 'kubectl apply -f deploy/deployment.yml'
        sh 'kubectl get all'
      }
    }

    stage('Cleaning Up') {
      steps {
        echo 'Cleaning up...'
        sh 'docker system prune'
      }
    }

  }
  environment {
    registry = 'fabioj/capstone'
    registryCredential = 'dockerhub'
    dockerImage = ''
  }
}