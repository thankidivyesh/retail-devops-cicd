pipeline {
    agent any

    environment {
        IMAGE_NAME = "abctehnologies"
        DOCKERHUB_USER = "thankidivyesh"
        CONTAINER_NAME = "abc-app"
        APP_PORT = "8081"
    }

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build Maven Project') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ${DOCKERHUB_USER}/${IMAGE_NAME}:${BUILD_NUMBER} .'
                sh 'docker tag ${DOCKERHUB_USER}/${IMAGE_NAME}:${BUILD_NUMBER} ${DOCKERHUB_USER}/${IMAGE_NAME}:latest'
            }
        }

        stage('Push Docker Image') {
            steps {
                withDockerRegistry([
    credentialsId: 'dockerhub-creds',
    url: 'https://index.docker.io/v1/'
]) {
                }
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                docker rm -f ${CONTAINER_NAME} || true
                docker run -d \
                  --name ${CONTAINER_NAME} \
                  -p ${APP_PORT}:8080 \
                  ${DOCKERHUB_USER}/${IMAGE_NAME}:${BUILD_NUMBER}
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
