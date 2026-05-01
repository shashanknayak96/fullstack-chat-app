pipeline {
    agent any

    environment {
        REGISTRY = "192.168.177.96:5001"
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
                '''
            }
        }

       stage('Push Image') {
            steps {
                sh '''
                docker push $REGISTRY/$IMAGE:$TAG
                '''
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh '''
                kubectl set image deployment/chatapp \
                chatapp=$REGISTRY/$IMAGE:$TAG
                '''
            }
        }

        stage('Verify Rollout') {
            steps {
                sh 'kubectl rollout status deployment/chatapp'
            }
        }
    }
}