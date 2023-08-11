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
        sh 'docker tag webdemo:${BUILD_NUMBER} bellsinclair/webdemo:${BUILD_NUMBER}'
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
