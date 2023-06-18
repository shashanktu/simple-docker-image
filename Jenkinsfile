pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/shashanktu/simple-docker-image.git'
            }
        }

        stage('Build and Push Docker Image') {
            steps {
                script {
                    def imageTag = "my-html-app:${env.BUILD_NUMBER}"
                    bat "docker build -t $imageTag ."
                    bat "docker tag $imageTag 670166063118.dkr.ecr.us-east-1.amazonaws.com/$imageTag"
                    bat "aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 670166063118.dkr.ecr.us-east-1.amazonaws.com"
                    bat "docker push 670166063118.dkr.ecr.us-east-1.amazonaws.com/$imageTag"
                }
            }
        }

    }
}

