cat > Jenkinsfile <<'EOF'
pipeline {
    agent any

    environment {
        IMAGE_NAME = "abctechnologies"
        DOCKERHUB_USER = "thankidivyesh"
        KUBE_CONFIG = "/var/lib/jenkins/.kube/config"
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
                withDockerRegistry([credentialsId: 'dockerhub-creds', url: '']) {
                    sh 'docker push ${DOCKERHUB_USER}/${IMAGE_NAME}:${BUILD_NUMBER}'
                    sh 'docker push ${DOCKERHUB_USER}/${IMAGE_NAME}:latest'
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh '''
                    export KUBECONFIG=${KUBE_CONFIG}

                    kubectl apply -f deployment.yaml
                    kubectl apply -f service.yaml

                    kubectl rollout status deployment/abc-deployment --timeout=120s
                    kubectl get pods
                    kubectl get svc
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
EOF
