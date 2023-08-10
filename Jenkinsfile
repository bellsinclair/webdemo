pipeline {
  agent any

  environment {

    }

  stages {
    stage('Run Shell and Set Env Variable') {
      steps {
        script {
          def mytag = sh(script: 'git rev-parse --short=6 HEAD')
          env.tag = mytag
          }

            }
        }
    stage('Docker Build') {
      steps {
        sh 'echo $mytag'
        sh 'docker build -t webdemo:$mytag .'
        sh 'docker images'
      }
    }
    stage('Docker-Tag') {
      steps {
        sh 'docker tag webdemo:$tag bellsinclair/webdemo:$mytag'
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
        sh 'docker push bellsinclair/webdemo:$$mytag'
      }
    }
    
  }
}
