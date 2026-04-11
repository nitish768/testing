pipeline {
    agent any

    stages {
        stage('Welcome') {
            steps {
                echo 'Jenkins + Docker pipeline start'
            }
        }

        stage('Check Docker') {
            steps {
                sh 'docker --version'
            }
        }
    }
}
