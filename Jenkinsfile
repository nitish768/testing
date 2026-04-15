// This defines a Jenkins pipeline (CI/CD workflow)
pipeline {

    // This tells Jenkins WHERE to run this pipeline
    // 'vm-agent' = your VM node label
    agent { label 'vm-agent' }

    stages {

        // Stage 1: Code checkout (GitHub se code lena)
        stage('Checkout Code') {
            steps {
                // This pulls code from the same repo where Jenkinsfile exists
                checkout scm
            }
        }

        // Stage 2: Verify Kubernetes connection
        stage('Check Kubernetes') {
            steps {
                // This runs command on VM agent
                sh 'kubectl get nodes'
                // Purpose: ensure cluster accessible hai
            }
        }

        // Stage 3: Deploy nginx
        stage('Deploy Nginx') {
            steps {
                sh '''
                # YAML ko dynamically create kar rahe hain
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

                # Apply YAML to Kubernetes
                kubectl apply -f nginx.yaml
                '''
                // Purpose: nginx deployment create/update karna
            }
        }

        // Stage 4: Verify deployment
        stage('Verify') {
            steps {
                sh 'kubectl get pods'
                // Purpose: check pods running or not
            }
        }
    }
}
