pipeline {
  agent any
  stages {
    stage('Buzz Build') {
      steps {
        sh 'echo I am a ${BUZZ_NAME}'
        sh '''
./jenkins/build.sh'''
        archiveArtifacts(artifacts: 'target/**/*.jar', fingerprint: true)
      }
    }

    stage('Buzz Test') {
      parallel {
        stage('Buzz Test') {
          steps {
            sh './jenkins/test-all.sh'
            junit '**/surefire-reports/**/*.xml'
          }
        }

        stage('Testing A') {
          steps {
            sh 'sleep 10; echo done'
          }
        }

        stage('Testing B') {
          steps {
            sh 'sleep 20; echo done'
          }
        }

      }
    }

  }
  environment {
    BUZZ_NAME = 'Worker bee'
  }
}