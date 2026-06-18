pipeline{
  agent any
  stages{
    stage('Checking Docker') {
      steps {
        sh 'docker version'
      }
    }
  }
  post {
    success { echo "Build Successful" }
    failure { echo "Build Failed" }
    always { echo "Cleanup Activities Completed" }
  }
}
