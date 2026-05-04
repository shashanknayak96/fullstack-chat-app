pipeline {
    agent any

    environment {
        REGISTRY = "172.20.0.3:5000"
        IMAGE = "chatapp-backend"
        TAG = "${BUILD_NUMBER}"
    }

    stages {

        stage('Check Files') {
            steps {
                sh 'ls -la'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                docker build -t $REGISTRY/$IMAGE:$TAG ./backend
                docker build -t $REGISTRY/$IMAGE:latest ./backend
                '''
            }
        }

       stage('Push Image') {
            steps {
                sh '''
                docker push $REGISTRY/$IMAGE:$TAG
                docker push $REGISTRY/$IMAGE:latest
                '''
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh '''
                kubectl set image deployment/backend-deployment \
                chatapp-backend=localhost:5001/$IMAGE:$TAG
                '''
            }
        }

        stage('Verify Rollout') {
            steps {
                sh 'kubectl rollout status deployment/backend-deployment'
            }
        }
    }
}