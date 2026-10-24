pipeline {
    agent any

    environment {
        AWS_REGION = 'ap-south-1'
        ECR_REPO = '455540676887.dkr.ecr.ap-south-1.amazonaws.com/vle7-app'
        IMAGE_NAME = 'vle7-app'
    }

    stages {

        stage('Build') {
            steps {
                echo 'Building the Docker image...'
                sh 'docker build -t $IMAGE_NAME:latest .'
            }
        }

        stage('Test') {
            steps {
                echo 'Checking the Docker image...'
                sh 'docker images $IMAGE_NAME'
            }
        }

        stage('ECR Login') {
            steps {
                echo 'Logging into Amazon ECR...'
                sh '''
                    aws ecr get-login-password --region $AWS_REGION | \
                    docker login --username AWS --password-stdin $ECR_REPO
                '''
            }
        }

        stage('Push to ECR') {
            steps {
                echo 'Tagging and pushing image to ECR...'
                sh '''
                    docker tag $IMAGE_NAME:latest $ECR_REPO:latest
                    docker push $ECR_REPO:latest
                '''
            }
        }
    }
}
