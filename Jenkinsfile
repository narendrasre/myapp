pipeline{
  agent any
  stages{
    stage('Check Kubectl') {
      steps {
        sh 'kubectl get pods -A'
      }
    }
    stage('Check Helm') {
      steps {
        sh 'helm list -A'
      }
    }
  }
  post {
    success { echo "Build Successful" }
    failure { echo "Build Failed" }
    always { echo "Cleanup Activities Completed" }
  }
}
