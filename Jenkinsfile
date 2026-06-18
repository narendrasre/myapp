pipeline{
  agent any
  stages{
    stage('Checkout') {
      steps {
        echo "Repository Checked out automatically"
      }
    }
    stage('Running Script') {
      steps {
        sh '''
        chmod +x app.sh
        ./app.sh
        '''
      }
    }
  }
  post {
    success { echo "Build Successful" }
    failure { echo "Build Failed" }
  }
}
