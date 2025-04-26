pipeline {
    agent any

    environment {
        IMAGE_NAME = 'adityanandan659/my-node-app'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/AdityaNandan193/my-node-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}")
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    script {
                        bat  "echo %DOCKER_PASS% | docker login -u %DOCKER_USER% --password-stdin"
                        bat "docker push %{IMAGE_NAME}%"
                    }
                }
            }
        }
    }
}
