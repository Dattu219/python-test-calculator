pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: 'main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Dattu219/python-test-calculator']]])
            }
        }
        stage('Docker-Compose-Build') {
            steps {
                sh 'curl -L https://github.com/docker/compose/releases/download/1.8.0/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose'
            }
        }
        stage('Build') {
            steps {
                git branch: 'main', url: 'https://github.com/Dattu219/python-test-calculator'
                sh '/usr/local/bin/docker-compose -f docker-compose.yml build --no-cache python-test-calculator'
            }
        }
        stage('Test') {
            steps {
                sh 'python3 -m pytest'
            }
        }
    }
}
