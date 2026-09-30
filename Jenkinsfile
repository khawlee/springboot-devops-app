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
                withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials',
                                                  usernameVariable: 'DOCKER_USER',
                                                  passwordVariable: 'DOCKER_PASS')]) {
                    sh '''
                        echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                        docker build -t khawle1/springboot-devops-app:latest .
                        docker push khawle1/springboot-devops-app:latest
                    '''
                }
            }
        }
    }
}