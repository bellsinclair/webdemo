pipeline {
  agent any
  stages {
    stage('Run Shell and Set Env Variable') {
      steps {
        script {
          def myOutput = sh(script: 'git rev-parse --short=6 HEAD')
          env.tag = myOutput
          }

            }
        }
    stage('Docker Build') {
      steps {
        sh 'echo "${env.tag}"'
        sh 'docker build -t webdemo:$tag .'
        sh 'docker images'
      }
    }
    stage('Docker-Tag') {
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
