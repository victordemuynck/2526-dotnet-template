pipeline {
    agent any 
    stages {
        stage('Preparation') {
            steps {
                catchError(buildResult: 'SUCCESS') {
                    sh 'docker stop rise-app'
                    sh 'docker rm rise-app'
                }
            }
        }
        stage('Build & Test') {
            agent {
                docker { 
                    image 'mcr.microsoft.com/dotnet/sdk:9.0'
                    reuseNode true
                }
            }
            steps {
                sh 'dotnet build'
                sh 'dotnet test'
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker build -t rise-image .'
                sh 'docker run -d -p 5001:8080 --name rise-app rise-image'
            }
        }
    }
}