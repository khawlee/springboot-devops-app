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
                    // تأكد من تكوين بيانات اعتماد دوكر هب (Docker Hub credentials) في Jenkins بالمعرف "dockerhub-credentials"
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