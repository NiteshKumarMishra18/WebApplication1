pipeline {
    agent any
    environment {
		ImageName = 'niteshkmishra/webapplication1'
        ImageTag = "v${env.BUILD_NUMBER}"
	}
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
                bat 'docker build -t niteshkmishra/webapplication1:%ImageTag% .'
            }
        }
        stage('dockerlogin') {
            steps {
                bat 'docker login -u niteshkmishra -p Docker@2024'
            }
        }
         stage('tagdockerimage') {
            steps {
                bat 'docker tag niteshkmishra/webapplication1:%ImageTag% niteshkmishra/webapplication1:latest'
            }
        }
         stage('pushdockerimage') {
            steps {
                bat 'docker push niteshkmishra/webapplication1:%ImageTag%'
            }
        }
        stage('deploy') {
            steps {
                bat '''docker ps -a
                       docker stop webapplication1-container
                       docker rm webapplication1-container
                       docker run -d -p 4999:80 --webapplication1-container niteshkmishra/webapplication1:%ImageTag%'''
            }
        }

        stage('clearworkspace') {
            steps {
                cleanWs()
            }
        }
    }
}
