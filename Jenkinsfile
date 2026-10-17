node {
    stage('Preparation') {
        catchError(buildResult: 'SUCCESS') {
            sh 'docker stop rise-app'
            sh 'docker rm rise-app'
        }
    }
    stage('Checkout') {
        checkout scm
    }
    stage('Build & Test') {
        sh 'dotnet build'
        sh 'dotnet test'
    }
    stage('Deploy') {
        sh 'docker build -t rise-image .'
        sh 'docker run -d -p 5001:8080 --name rise-app rise-image'
    }
}