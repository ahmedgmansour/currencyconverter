pipeline {
    agent any
    environment {
        DOCKERHUB_USERNAME = credentials('dockerhub-username')
        DOCKERHUB_TOKEN = credentials('dockerhub-token')
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Login to DockerHub') {
            steps {
                sh """
                echo ${DOCKERHUB_TOKEN} | docker login -u ${DOCKERHUB_USERNAME} --password-stdin
                """
            }
        }
        stage('Build and Push Docker Image') {
            steps {
                sh """
                docker build -t mabusaa/argocd-course-webapp:${env.GIT_COMMIT} -f WebApplication1/Dockerfile .
                docker push mabusaa/argocd-course-webapp:${env.GIT_COMMIT}
                """
            }
        }
    }
}
