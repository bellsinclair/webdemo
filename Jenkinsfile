pipeline {
  agent any

  stages {
    stage('Run Shell and Set Env Variable') {
      steps {
        script {
          def myOutput = sh(script: 'git rev-parse --short=6 HEAD')
          env.tag = mytag
          }

            }
        }
    
  }
}
