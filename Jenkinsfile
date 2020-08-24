pipeline {
  agent any
  stages {
    stage('Buzz Build') {
      steps {
        sh './jenkins/build.sh'
        archiveArtifacts(artifacts: 'target/**/*.jar', fingerprint: true)
        echo 'I am a $BUZZ_NAME'
      }
    }

    stage('Buzz Test') {
      steps {
        sh './jenkins/test-all.sh'
        junit '**/surefire-reports/**/*.xml'
      }
    }

  }
  environment {
    BUZZ_NAME = 'Worker bee'
  }
}