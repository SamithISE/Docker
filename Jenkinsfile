pipeline {
    agent any

    environment {
        IMAGE_NAME = "samithhm/demo-app"
    }

    stages {

        stage('Build Java App') {
            steps {
                bat 'javac demo.java'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat "docker build -t %IMAGE_NAME%:v1 ."
            }
        }

        stage('Push to DockerHub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerID',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS'
                )]) {
                    bat 'echo %PASS% | docker login -u %USER% --password-stdin'
                    bat "docker push %IMAGE_NAME%:v1"
                }
            }
        }
    }
}
