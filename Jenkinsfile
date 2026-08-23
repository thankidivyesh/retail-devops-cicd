pipeline {
    agent any

    environment {
        IMAGE_NAME = "abctechnologies"
        DOCKERHUB_USER = "thankidivyesh"
        KUBECONFIG = "/var/lib/jenkins/.kube/config"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/thankidivyesh/retail-devops-cicd.git'
            }
        }

        stage('Build Maven Project') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Prepare WAR') {
            steps {
                sh 'cp target/ABCtechnologies-1.0.war .'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
<<<<<<< HEAD
                    docker build \
                    -t ${DOCKERHUB_USER}/${IMAGE_NAME}:${BUILD_NUMBER} \
                    .

                    docker tag \
                    ${DOCKERHUB_USER}/${IMAGE_NAME}:${BUILD_NUMBER} \
                    ${DOCKERHUB_USER}/${IMAGE_NAME}:latest
=======
                docker build -t ${DOCKERHUB_USER}/${IMAGE_NAME}:${BUILD_NUMBER} .
                docker tag ${DOCKERHUB_USER}/${IMAGE_NAME}:${BUILD_NUMBER} ${DOCKERHUB_USER}/${IMAGE_NAME}:latest
>>>>>>> c57adab (Add Kubernetes deployment to Jenkins pipeline)
                '''
            }
        }

        stage('Push Docker Image') {
            steps {
                withDockerRegistry([
                    credentialsId: 'dockerhub-creds',
                    url: 'https://index.docker.io/v1/'
                ]) {
                    sh '''
<<<<<<< HEAD
                        docker push ${DOCKERHUB_USER}/${IMAGE_NAME}:${BUILD_NUMBER}
                        docker push ${DOCKERHUB_USER}/${IMAGE_NAME}:latest
=======
                    docker push ${DOCKERHUB_USER}/${IMAGE_NAME}:${BUILD_NUMBER}
                    docker push ${DOCKERHUB_USER}/${IMAGE_NAME}:latest
>>>>>>> c57adab (Add Kubernetes deployment to Jenkins pipeline)
                    '''
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh '''
<<<<<<< HEAD
                    docker rm -f ${CONTAINER_NAME} || true

                    docker run -d \
                    --name ${CONTAINER_NAME} \
                    -p ${APP_PORT}:8080 \
                    ${DOCKERHUB_USER}/${IMAGE_NAME}:${BUILD_NUMBER}
=======
                kubectl --kubeconfig=${KUBECONFIG} apply -f deployment.yaml
                kubectl --kubeconfig=${KUBECONFIG} apply -f service.yaml

                kubectl --kubeconfig=${KUBECONFIG} rollout restart deployment/abc-deployment

                kubectl --kubeconfig=${KUBECONFIG} rollout status deployment/abc-deployment --timeout=120s
                '''
            }
        }

        stage('Verify Kubernetes') {
            steps {
                sh '''
                kubectl --kubeconfig=${KUBECONFIG} get nodes
                kubectl --kubeconfig=${KUBECONFIG} get pods
                kubectl --kubeconfig=${KUBECONFIG} get services
>>>>>>> c57adab (Add Kubernetes deployment to Jenkins pipeline)
                '''
            }
        }
    }

    post {
        success {
            echo 'CI/CD Pipeline completed successfully!'
        }

        failure {
            echo 'Pipeline failed. Check Console Output.'
        }
    }
}
