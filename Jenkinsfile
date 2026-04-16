pipeline {
    agent { label 'nitishbabu' }

    parameters {
        choice(name: 'ENV', choices: ['nitish-dev', 'nitish-prod'], description: 'Select Environment')
    }

    environment {
        PATH = "/usr/bin:/usr/local/bin:/snap/bin:/usr/bin:/bin:$PATH"
        IMAGE_NAME = "nitishsingh/jenkins"
        TAG = "${BUILD_NUMBER}"
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
                echo "Building Docker image..."
                docker build -t $IMAGE_NAME:$TAG .
                '''
            }
        }

        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'docker-hub-cred',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh """
                    echo \$DOCKER_PASS | docker login -u \$DOCKER_USER --password-stdin
                    """
                }
            }
        }

        stage('Push Image') {
            steps {
                sh '''
                echo "Pushing image..."
                docker push $IMAGE_NAME:$TAG
                '''
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh """
                echo "Deploying to ${params.ENV}..."

                cat <<EOF | kubectl apply -n ${params.ENV} -f -
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: $IMAGE_NAME:$TAG
        ports:
        - containerPort: 80
EOF
                """
            }
        }

        stage('Verify') {
            steps {
                sh """
                echo "Checking pods in ${params.ENV}..."
                kubectl get pods -n ${params.ENV}
                """
            }
        }
    }
}
