pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Code checked out from GitHub'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t cicd-demo:latest .'
            }
        }

        stage('Test Application') {
            steps {
                sh '''
                docker run -d -p 5000:5000 --name test-app cicd-demo:latest
                sleep 5
                curl http://localhost:5000
                docker rm -f test-app
                '''
            }
        }

        stage('Deploy Application') {
            steps {
                sh '''
                docker rm -f prod-app || true
                docker run -d -p 80:5000 --name prod-app cicd-demo:latest
                '''
            }
        }
    }
}

