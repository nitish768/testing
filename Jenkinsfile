pipeline {
    agent { label 'vm-agent' }

    stages {
        stage('Check Node') {
            steps {
                sh '''
                echo "Running on:"
                hostname
                '''
            }
        }
    }
}
