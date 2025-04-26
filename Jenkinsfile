pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'adityanandan659/my-node-app' 
    }

    stages {
        stage('Clone Repo') {
            steps {
                 git branch: 'main', url: 'https://github.com/AdityaNandan193/my-node-app.git'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %DOCKER_IMAGE% .'
            }
        }
        
        stage('Push Docker Image to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    bat """
                        echo %PASSWORD% | docker login -u %USERNAME% --password-stdin
                        docker push %DOCKER_IMAGE%
                    """
                }
            }
        }
    }
}
