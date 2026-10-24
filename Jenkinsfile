pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Building the application...'
                sh 'docker build -t vle7-app .'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing the Docker image...'
                sh 'docker images vle7-app'
            }
        }
    }
}
