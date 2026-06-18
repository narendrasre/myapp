pipeline{
  agent any
  stages{
    stage('Check Kubectl') {
      steps {
        sh 'kubectl'
      }
    }
    stage('Check Helm') {
      steps {
        sh 'helm version'
      }
    }
  }
  post {
    success { echo "Build Successful" }
    failure { echo "Build Failed" }
    always { echo "Cleanup Activities Completed" }
  }
}
