pipeline {
  agent any
  environment {
        DOCKER_CRED = credentials('dockerhub-credentials')
            }
  stages {
    stage('Docker Build') {
      steps {
        sh 'echo V${BUILD_ID}'
        sh 'dockerg build -t webdemo:V${BUILD_ID} .'
        sh 'docker images'
      }
    }
    stage('Docker-Tag') {
      steps {
        sh 'docker tag webdemo:V${BUILD_ID} bellsinclair/webdemo:V${BUILD_ID}'
        sh 'docker images'
      }
    }
    stage('Docker Login') {
      steps {
        sh 'echo "$DOCKER_CRED_PSW" | docker login -u $DOCKER_CRED_USR --password-stdin'
        }
        }
    stage('Docker push') {
      steps {
        sh 'docker push bellsinclair/webdemo:V${BUILD_ID}'
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
