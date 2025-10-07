pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('docker-hub-cred')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/sunil-th/docker-011.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t sunildev99/docker-01:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push sunildev99/docker-01:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}

