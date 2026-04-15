pipeline {
    agent { label 'vm-ssh' }

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
