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
                sh '/usr/local/bin/docker --version'
            }
        }

        stage('Build Image') {
            steps {
                sh '/usr/local/bin/docker build -t nitish-nginx-app .'
            }
        }
    }
}
