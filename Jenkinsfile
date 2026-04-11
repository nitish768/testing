pipeline {
    agent any

    stages {
        stage('Welcome to NitishDocker') {
            steps {
                echo 'Jenkins + Docker pipeline start'
            }
        }

        stage('Check Docker') {
            steps {
                sh '/usr/local/bin/docker --version'
            }
        }
    }
}
