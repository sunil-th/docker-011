pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('docker-jenkins')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/prakash6333/docker-nodejs.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t prakash6333/nodeapp:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push prakash6333/nodeapp:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}

