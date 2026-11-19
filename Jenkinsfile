pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out Week 11 E-commerce project'
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                    python3 -m venv venv
                    . venv/bin/activate
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Test') {
            steps {
                sh '''
                    . venv/bin/activate
                    python3 -m pytest
                '''
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t week11-ecommerce .'
            }
        }

        stage('Deployment') {
            steps {
                sh '''
                    docker rm -f week11-jenkins-app || true
                    docker run -d --name week11-jenkins-app -p 8084:80 week11-ecommerce
                '''
            }
        }

        stage('Verify') {
            steps {
                sh 'docker ps'
            }
        }
    }
}
