pipeline{
  agent any
  stages('Tests') {
    parallel {
      stage('Unit Test') {
        steps {
          echo "Running Unit Tests"
        }
      }
      stage('Security Scan') {
        steps {
          echo "Running security scan"
        }
      }
    }
  }
}
