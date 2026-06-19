pipeline {

    agent any

    parameters {
        string(
            name: 'IMAGE_TAG',
            defaultValue: '1.0.0',
            description: 'Docker image tag'
        )
    }

    environment {
        REPO_NAME   = "narendra115c/demo-app"
        RELEASE_NAME = "demo-app"
        NAMESPACE    = "demo"
    }

    stages {

        stage('Checkout') {
            steps {
                echo "Source code already checked out"
            }
        }

        stage('Parallel Validation') {

            parallel {

                stage('Unit Tests') {
                    steps {
                        sh '''
                        echo "Running unit tests..."
                        sleep 10
                        '''
                    }
                }

                stage('Security Scan') {
                    steps {
                        sh '''
                        echo "Running security scan..."
                        sleep 10
                        '''
                    }
                }

                stage('Lint Check') {
                    steps {
                        sh '''
                        echo "Running lint checks..."
                        sleep 10
                        '''
                    }
                }

            }
        }

        stage('Build Image') {
            steps {
                sh """
                docker build \
                  -t ${REPO_NAME}:${params.IMAGE_TAG} .
                """
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
                    echo "$DOCKER_PASS" | docker login \
                    -u "$DOCKER_USER" \
                    --password-stdin
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
                helm upgrade --install ${RELEASE_NAME} charts/demo-app \
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
                kubectl get pods -n ${NAMESPACE}
                kubectl get svc -n ${NAMESPACE}
                """
            }
        }
    }

    post {

        success {
            echo "Deployment Successful"
        }

        failure {
            echo "Deployment Failed"
        }

        always {
            echo "Pipeline execution finished"
        }

    }
}
