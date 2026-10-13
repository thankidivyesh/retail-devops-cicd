pipeline {
    agent any

    environment {
        IMAGE_NAME = "thankidivyesh/abctechnologies"
        KUBECONFIG = "/var/lib/jenkins/.kube/config"
    }

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Maven Build') {
            steps {
                sh 'mvn clean package'
                sh 'test -f target/ABCtechnologies-1.0.war'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ${IMAGE_NAME}:${BUILD_NUMBER} .'
            }
        }

        stage('Push Docker Image') {
            steps {
                withDockerRegistry([credentialsId: 'dockerhub-creds']) {
                    sh 'docker push ${IMAGE_NAME}:${BUILD_NUMBER}'
                }
            }
        }

        stage('Load Image into Kind') {
            steps {
                sh 'kind load docker-image ${IMAGE_NAME}:${BUILD_NUMBER} --name retail-cluster'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh '''
                    kubectl set image deployment/abc-deployment abc-app=${IMAGE_NAME}:${BUILD_NUMBER}
                    kubectl rollout status deployment/abc-deployment --timeout=180s
                    kubectl get pods
                    kubectl get svc abc-service
                '''
            }
        }
    }

    post {
        success {
            echo 'CI/CD pipeline completed successfully.'
        }
        failure {
            echo 'CI/CD pipeline failed. Check the stage logs.'
        }
    }
}
