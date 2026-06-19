pipeline{
  agent any
  parameters {
    string ( name: 'IMAGE_TAG', defaultValue: '1.0.0', description: 'Docker Image Tag' )
  }
  environment { REPO_NAME = "narendra115c/demo-app" RELEASE_NAME = "demo-app"  NAMESPACE = "demo" }
  stages{
    stage('Checkout') {
      steps {
        echo "Checking out source code."
      }
    }
    stage('Build Image') {
      steps {
        sh '''
        docker build -t ${REPO_NAME}:${params.IMAGE_TAG} .
        '''
      }
    }
    stage('DockerHub Login') {
      steps {
        withCredentials([
          usernamePassword(
            credentialsId: 'DockerHub',
            usernameVariable: 'DOCKER_USER',
            passwordVariable: 'DOCKER_PASS'
          )
        ]) {
          sh '''
          echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
          '''
        }
      }
    }
    stage('Push Image') {
      steps {
        sh """
        docker push ${REPO_NAME}:${params.IMAGE_TAG}
        """
      }
    }
    stage('Deploy') {
      steps {
        sh """
        helm upgrade --install ${RELEASE_NAME} demo-app \
          --namespace ${NAMESPACE} \
          --create-namespace \
          --set image.repository=${REPO_NAME} \
          --set image.tag=${params.IMAGE_TAG}
          """
      }
    }
    stage('Verify Deployment') {
      steps {
        sh """
        kubectl get pods --namespace ${NAMESPACE}
        kubectl get svc --namespace ${NAMESPACE}
        """
      }
    }
  }
  post {
    success { echo "Deployment Successfull" }
    failure { echo "Deployment Failed" }
    always { echo "Pipeline execution finished" }
  }
}
