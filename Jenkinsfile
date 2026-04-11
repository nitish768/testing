pipeline {
    agent any

    stages {
        stage('Welcome') {
            steps {
                echo '🚀 Aapka Jenkins ki duniya me swaagat hai!'
                echo 'Welcome Nitish 👑 — Pipeline successfully started'
            }
        }

        stage('Clone') {
            steps {
                echo '📦 Code clone ho raha hai...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo '⚙️ Build process start ho gaya...'
                sh 'echo Build done successfully ✅'
            }
        }

        stage('Finish') {
            steps {
                echo '🎉 Pipeline completed successfully!'
            }
        }
    }
}
