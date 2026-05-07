pipeline {
    agent any

    stages {
        stage('Train Model') {
            steps {
                sh '''
                    python3 train.py
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                    docker build -t ml-pipeline-image .
                '''
            }
        }

        stage('Run Docker Container') {
            steps {
                sh '''
                    docker stop ml-pipeline-app || true
                    docker rm ml-pipeline-app || true
                    docker run -d --name ml-pipeline-app -p 8000:8000 ml-pipeline-image
                '''
            }
        }
    }
}
