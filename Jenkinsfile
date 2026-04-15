pipeline {
    agent { label 'nitishbabu' }

    environment {
        PATH = "/snap/bin:/usr/local/bin:/usr/bin:/bin:$PATH"
    }

    stages {

        stage('Check Node') {
            steps {
                sh '''
                echo "Running on:"
                hostname
                '''
            }
        }

        stage('Check Kubernetes') {
            steps {
                sh '''
                echo "Checking cluster..."
                kubectl get nodes
                '''
            }
        }

        stage('Deploy Nginx') {
            steps {
                sh '''
                echo "Deploying nginx..."

                cat <<EOF > nginx.yaml
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
                        image: nginx
                        ports:
                        - containerPort: 80
                EOF

                kubectl apply -f nginx.yaml
                '''
            }
        }

        stage('Verify Pods') {
            steps {
                sh '''
                echo "Pods status:"
                kubectl get pods
                '''
            }
        }
    }
}
