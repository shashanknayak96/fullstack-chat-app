pipeline {
    agent any

    environment {
        REGISTRY = "localhost:5001"
        IMAGE = "chatapp-backend"
        TAG = "${BUILD_NUMBER}"
    }

    stages {

        stage('Check Files') {
            steps {
                sh 'ls -la'
            }
        }

        stage('Build Docker') {
            steps {
                sh 'docker build -t localhost:5000/my-app:test .'
            }
        }

        stage('Push Docker') {
            steps {
                sh '''
                docker push $REGISTRY/$IMAGE:$TAG
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                kubectl set image deployment/my-app \
                my-app=$REGISTRY/$IMAGE:$TAG
                '''
            }
        }
    }
}