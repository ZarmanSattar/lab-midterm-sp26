pipeline {
    agent any

    stages {
        stage('Fetch Data from GitHub') {
            steps {
                sh '''
                    rsync -av --exclude='.git' ${WORKSPACE}/ /home/ubuntu/lab-midterm-sp26/
                '''
            }
        }

        stage('Train Model') {
            steps {
                sh '''
                    cd /home/ubuntu/lab-midterm-sp26
                    python3 train.py
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                    cd /home/ubuntu/lab-midterm-sp26
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
