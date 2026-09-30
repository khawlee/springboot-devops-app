pipeline {
agent any

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/khawlee/springboot-devops-app.git'
            }
        }

        stage('Build Maven Project') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Build & Push Docker Image') {
            steps {
                script {
                    // Assurez-vous d'avoir configuré les credentials Docker dans Jenkins avec l'ID "dockerhub-credentials"
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-credentials') {
                        def customImage = docker.image("khawle1/springboot-devops-app:latest")
                        customImage.build()
                        customImage.push()
                    }
                }
            }
        }
    }
}