pipeline {
    agent { label 'nitishbabu' }

    environment {
        PATH = "/snap/bin:/usr/local/bin:/usr/bin:/bin:$PATH"
        IMAGE_NAME = "nitish768/my-nginx-app"
        TAG = "latest"
    }

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                docker build -t $IMAGE_NAME:$TAG .
                '''
            }
        }

        stage('Docker Login') {
            steps {
                sh '''
                docker login -u <your-username> -p <your-password>
                '''
            }
        }

        stage('Push Image') {
            steps {
                sh '''
                docker push $IMAGE_NAME:$TAG
                '''
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh '''
                kubectl set image deployment/nginx-deployment \
                nginx=$IMAGE_NAME:$TAG
                '''
            }
        }

        stage('Verify') {
            steps {
                sh '''
                kubectl get pods
                '''
            }
        }
    }
}
