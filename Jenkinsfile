pipeline {
    agent any

    environment {
        IMAGE_NAME = "samithhm/demo-app"
    }

    stages {

        stage('Clone Code') {
            steps {
                git branch: 'main', url: 'https://github.com/SamithISE/Docker.git'
            }
        }

        stage('Build Java App') {
            steps {
                bat 'javac demo.java'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}:latest")
                }
            }
        }

        stage('Login & Push to DockerHub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerID',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS'
                )]) {
                   bat 'echo %PASS% | docker login -u %USER% --password-stdin'
                    bat "docker push ${IMAGE_NAME}:v1"
                }
            }
        }
    }
}
