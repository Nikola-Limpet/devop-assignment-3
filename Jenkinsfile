pipeline {
    agent { label 'agen1' }

    environment {
        APP_NAME = 'node-api-container'
        IMAGE_NAME = 'node-api-image'
        APP_PORT = '3000'
        REPO_URL = 'https://github.com/Nikola-Limpet/devop-assignment-3.git'
    }

    stages {
        stage('Clean Workspace') {
            steps {
                deleteDir()
            }
        }

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: "${REPO_URL}"
            }
        }

        stage('Show Workspace') {
            steps {
                sh 'echo WORKSPACE=$WORKSPACE'
                sh 'pwd'
                sh 'ls -la'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ${IMAGE_NAME}:latest .'
            }
        }

        stage('Remove Old Container') {
            steps {
                sh 'docker rm -f ${APP_NAME} || true'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d --name ${APP_NAME} -p ${APP_PORT}:3000 ${IMAGE_NAME}:latest'
            }
        }

        stage('Verify Container') {
            steps {
                sh 'docker ps'
            }
        }
    }
}
