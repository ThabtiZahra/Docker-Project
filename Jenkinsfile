pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                script {
                    checkout scmGit(branches:[[name:'*/main']], extensions:[], userRemoteConfigs:[[url:'https://github.com/ThabtiZahra/Docker-Project.git']])
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
