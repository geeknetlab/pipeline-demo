pipeline {
  agent none
  stages {
    stage('Buzz Build') {
      parallel {
        stage('Build Java 7') {
          agent {
            node {
              label 'java7'
            }

          }
          steps {
            sh 'echo I am a ${BUZZ_NAME}'
            sh '''
./jenkins/build.sh'''
            archiveArtifacts(artifacts: 'target/**/*.jar', fingerprint: true)
          }
        }

        stage('Build Java 8') {
          agent {
            node {
              label 'java8'
            }

          }
          environment {
            BUZZ_NAME = 'Java 8 Bee'
          }
          steps {
            sh './jenkins/build.sh'
            archiveArtifacts(artifacts: 'target/*.jar', fingerprint: true)
            sh 'echo I am a ${BUZZ_NAME}'
          }
        }

      }
    }

    stage('Buzz Test') {
      parallel {
        stage('Testing A') {
          agent {
            node {
              label 'java7'
            }

          }
          steps {
            sh './jenkins/test-all.sh'
            junit '**/surefire-reports/**/*.xml'
          }
        }

        stage('Testing B') {
          agent {
            node {
              label 'java7'
            }

          }
          steps {
            sh 'sleep 10; echo done'
          }
        }

      }
    }

  }
  environment {
    BUZZ_NAME = 'Worker bee'
  }
}