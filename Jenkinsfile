pipeline {
    agent any

    environment {
        AWS_REGION = "us-east-1"
        ACCOUNT_ID = "245324547477"
        IMAGE_NAME = "245324547477.dkr.ecr.us-east-1.amazonaws.com/eco-lume"
        REGISTRY = "https://245324547477.dkr.ecr.us-east-1.amazonaws.com"
    }

    stages {

        stage('Fetch Code') {
            steps {
                git branch: 'main', url: 'https://github.com/SANJAI-S1/eco-lume.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("${IMAGE_NAME}:${BUILD_NUMBER}", ".")
                }
            }
        }

        stage('Login & Push to ECR') {
            steps {
                script {
                    docker.withRegistry("${REGISTRY}", "ecr:us-east-1:awsk") {
                        dockerImage.push("${BUILD_NUMBER}")
                        dockerImage.push("latest")
                    }
                }
            }
        }
    }
}
