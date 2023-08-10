pipeline {
  agent any
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
        sh 'echo ${BUILD_NUMBER}'
        sh 'docker build -t webdemo:${BUILD_NUMBER} .'
        sh 'docker images'
      }
    }
    stage('Docker-Tag') {
      steps {
        sh 'docker tag webdemo:$tag bellsinclair/webdemo:${BUILD_NUMBER}'
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
        sh 'docker push bellsinclair/webdemo:$${BUILD_NUMBER}'
      }
    }
    
  }
}
