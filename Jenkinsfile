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
        sh 'echo ${BUILD_ID}'
        sh 'docker build -t webdemo:${BUILD_ID} .'
        sh 'docker images'
      }
    }
    stage('Docker-Tag') {
      steps {
        sh 'docker tag webdemo:${BUILD_ID} bellsinclair/webdemo:${BUILD_ID}'
        sh 'docker images'
      }
    }
    stage('Docker Login') {
      environment {
        DOCKER_CRED = credentials('dockerhub-credentials')
            }
      steps {
        sh 'echo "$DOCKER_CRED_PSW" | docker login -u $DOCKER_CRED_USR --password-stdin'
        }
        }
    stage('Docker push') {
      steps {
        sh 'docker push bellsinclair/webdemo:${BUILD_ID}'
      }
    }
    
  }
  post {
        always {
            // This will always send a message to the Slack channel
            slackSend (color: '#FFFF00', message: "Build ${currentBuild.fullDisplayName} finished with result: ${currentBuild.result}")
        }
        failure {
            // This will only send a message if the build fails
            slackSend (color: '#FF0000', message: "Build ${currentBuild.fullDisplayName} failed!")
        }
        success {
            // This will only send a message if the build is successful
            slackSend (color: '#00FF00', message: "Build ${currentBuild.fullDisplayName} succeeded!")
        }
  
     }
}
