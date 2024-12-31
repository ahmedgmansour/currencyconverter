pipeline {
    agent any
    environment {
        DOCKERHUB_USERNAME = credentials('dockerhub-username')
        DOCKERHUB_TOKEN = credentials('dockerhub-token')
    }
    stages {
        stage('Checkout from Git'){
            steps{
                git branch: 'main', url: 'https://github.com/ahmedgmansour/currencyconverter.git'
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
                docker build -t ahmedgmansour/currencyconverter .
                docker push ahmedgmansour/currencyconverter:latest
                """
            }
        }
    }
}
