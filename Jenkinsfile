node{
    stage('Build') {
        echo 'Build my code'
        git branch: 'scripted-pipeline', credentialsId: 'gkn_github', url: 'git@github.com:geeknetlab/pipeline-demo.git'
        sh label: '', script: './jenkins/build.sh'
        archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
      }

    stage('Test') {
      parallel {
        stage('Backend'){
        sh './jenkins/test-backend.sh'
        junit 'target/surefire-reports/**/TEST*.xml'
      }
      stage('Frontend'){
        sh './jenkins/test-frontend.sh'
        junit 'target/test-results/**/TEST*.xml'        
      }
      stage('Performance'){
        sh './jenkins/test-performance.sh'
      }
      stage('Static'){
        sh './jenkins/test-static.sh'
      }
     }
    }
    stage('Deploy'){
      sh './jenkins/deploy.sh staging'
  }
}
