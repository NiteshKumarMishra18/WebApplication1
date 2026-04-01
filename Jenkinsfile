pipeline {
    agent any

    stages {
    stage('checkout') {
            steps {
                checkout scm 
            }
        }
        stage('build') {
            steps {
                bat 'dotnet build WebApplication1.csproj'
            }
        }
        stage('publish') {
            steps {
                bat 'dotnet publish WebApplication1.csproj -c Release -o published'
            }
        }
        stage('builddockerimage') {
            steps {
                bat 'docker build -t niteshkmishra/webapplication1:latest .'
            }
        }
        stage('dockerlogin') {
            steps {
                bat 'docker login -u niteshkmishra -p Docker@2024'
            }
        }
         stage('tagdockerimage') {
            steps {
                bat 'docker tag niteshkmishra/webapplication1:latest niteshkmishra/webapplication1:latest1'
            }
        }
         stage('pushdockerimage') {
            steps {
                bat 'docker push niteshkmishra/webapplication1:latest'
            }
        }
    }
}
