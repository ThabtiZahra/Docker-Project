pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                script {
                    try {
                        checkout scm
                    } catch (Exception e) {
                        echo "Error checking out code: ${e.message}"
                        currentBuild.result = 'FAILURE'
                        error("Failed to checkout code")
                    }
                }
            }
        }

        stage('Deploy Services') {
            steps {
                script {
                    try {
                        sh "docker-compose up -d"
                    } catch (Exception e) {
                        echo "Error deploying services: ${e.message}"
                        currentBuild.result = 'FAILURE'
                        error("Failed to deploy services")
                    }
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

