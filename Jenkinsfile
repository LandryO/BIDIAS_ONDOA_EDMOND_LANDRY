pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-id') // Identifiant DockerHub dans Jenkins
        IMAGE_NAME = 'ton_dockerhub/ton_nom-flask-app'     // Remplace par ton DockerHub
        GIT_REPO = 'https://github.com/LandryO/TP_Docker.git'
    }
    stages {
        stage('Clonage') {
            steps {
                git branch: 'main', url: "${env.GIT_REPO}"
            }
        }
        stage('Construction de l\'image Docker') {
            steps {
                script {
                    docker.build("${env.IMAGE_NAME}:latest")
                }
            }
        }
        stage('Publication sur DockerHub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', "${env.DOCKERHUB_CREDENTIALS}") {
                        docker.image("${env.IMAGE_NAME}:latest").push()
                    }
                }
            }
        }
    }
}
