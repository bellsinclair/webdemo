pipeline {
  agent any
  stages {
    stage('Docker Build') {
      steps {
        sh 'tag="git rev-parse --short=6 HEAD"'
        sh 'docker build -t webdemo:$tag .'
        sh 'docker images'
      }
    }
    stage('Docker Tag') {
      steps {
        sh 'docker tag webdemo:$tag bellsinclair/webdemo:$tag'
        sh 'docker images'
      }
    }
    stage('Docker login') {
      steps {
        sh 'echo $DP |docker login -u $DL --password-stdin'
      }
    }
    stage('Docker push') {
      steps {
        sh 'docker push bellsinclair/webdemo:$tag'
      }
    }
    
  }
}
