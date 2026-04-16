pipeline {
    agent any

    environment {
      DOCKERHUB_CREDENTIALS='new_credentials_c1'
      IMAGE_NAME = 'sandhyag4/new_docker_image'
      }

    stages {

        stage('Build java application') {
            steps {
                bat 'javac HelloWorld.java'
            }
        }
      stage('Run java program') {
            steps {
                bat 'java HelloWorld'
            }
        }

      stage('Build Docker Image') {
            steps {
                bat 'docker build -t %IMAGE_NAME%:latest .'
            }
        }
   


        stage('Login to DockerHub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'new_credentials_c1',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS'
                )]) {
                    bat 'echo %PASS%| docker login -u %USER% --password-stdin'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                bat 'docker push %IMAGE_NAME%:latest'
            }
        }
    }
}
