pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Building...'
      }
    }
    stage('Test') {
      steps {
        echo 'Testing Testing...'
      }
    }
    stage('Deploy') {
      steps {
        echo 'Deploying...'
      }
    }
    stage('Docker pull') {
      steps {
        sh 'docker pull jenkins/jenkins'
        sh 'docker images'
      }
    }
    stage('Docker run') {
      steps {
        sh 'docker run -p 8080:8080 -p 50000:50000 jenkins/jenkins:lts'
      }
    }
    
  }
}
