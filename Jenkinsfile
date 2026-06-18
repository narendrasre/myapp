pipeline{
  agent any
  stages{
    stage('Checkout') {
      steps {
        echo "Checkout successful"
      }
    }
    stage('Kubernetes') {
      steps {
        sh '''
        kubectl get pods -n dev
        '''
      }
    }
  }
  post {
    success { echo "Build Successful" }
    failure { echo "Build Failed" }
    always { echo "Cleanup Activities Completed" }
  }
}
