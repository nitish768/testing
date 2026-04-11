pipeline {
    agent any

    stages {
        stage('Welcome to nitish docker') {
            steps {
                echo 'Jenkins + Docker pipeline start'
            }
        }

        stage('Clone') {
            steps {
                checkout scm
            }
        }

        stage('Check Docker nitish docker running') {
            steps {
                sh 'docker --version'
            }
        }
    }
}
