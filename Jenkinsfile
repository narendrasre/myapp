pipeline{
  agent any
  stages{
    stage('Checkout') {
      steps {
        echo "Repository Checked out successfull"
      }
    }
    stage('Build') {
      steps {
        sh '''
        echo "Building application..."
        sleep 5
        '''
      }
    }
    stage('Test') {
      steps {
        sh '''
        echo "Running Tests..."
        exit 1
        '''
      }
    }
    stage('Package') {
      steps {
        sh '''
        echo "Packaging application..."
        sleep 5
        '''
      }
    }
    stage('Deploy') {
      steps {
        sh '''
        echo "Deploying application..."
        sleep 5
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
