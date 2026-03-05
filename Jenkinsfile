pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/YOUR_USERNAME/foodexpress-api.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Test') {
            steps {
                sh 'npm test'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t foodexpress-api .'
            }
        }

        stage('Deploy') {
            steps {
                sh 'docker stop foodexpress-api || true'
                sh 'docker rm foodexpress-api || true'
                sh 'docker run -d --name foodexpress-api -p 5000:5000 foodexpress-api'
            }
        }
    }
}
