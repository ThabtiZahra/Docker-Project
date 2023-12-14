pipeline {
    agent any

    environment {
        DOCKER_IMAGE_SVM = 'thabtizahra/svm_service:latest'
        DOCKER_IMAGE_VGG19 = 'thabtizahra/vgg19_service:latest'
        DOCKER_IMAGE_FRONT = 'thabtizahra/front_service:latest'
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    checkout scm
                }
            }
        }

        stage('Build and Push Docker Images') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub-credentials') {
                        sh "docker-compose build"
                        sh "docker-compose push"
                    }
                }
            }
        }

        stage('Deploy Services') {
            steps {
                script {
                    sh "docker-compose up -d"
                }
            }
        }
    }

    post {
        always {
            script {
                sh "docker-compose down"
            }
        }
    }
}
