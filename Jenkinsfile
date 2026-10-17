pipeline {
    agent any
    stages {
        stage('Build') {
            agent {
                docker {
                    image 'mcr.microsoft.com/dotnet/sdk:9.0'
                    reuseNode true
                }
            }
            steps {
                sh 'dotnet build'
            }
        }
        stage('Test') {
            agent {
                docker {
                    image 'mcr.microsoft.com/dotnet/sdk:9.0'
                    reuseNode true
                }
            }
            steps {
                sh 'dotnet test --no-build'
            }
        }
        stage('Cleanup') {
            steps {
                sh 'docker rm -f rise-app || true'
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