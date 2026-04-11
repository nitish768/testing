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
                sh '''
                    mkdir -p $WORKSPACE/.docker-tmp
                    echo '{}' > $WORKSPACE/.docker-tmp/config.json
                    DOCKER_CONFIG=$WORKSPACE/.docker-tmp /usr/local/bin/docker build -t nitish-nginx-app .
                '''
            }
        }
    }
}
