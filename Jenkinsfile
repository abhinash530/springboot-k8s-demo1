pipeline {
    agent any

    tools {
        jdk 'java'
        maven 'Maven'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/abhinash530/springboot-k8s-demo1.git'
            }
        }

        stage('Build Maven') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t springboot-k8s-demo1:1.0 .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub',
                        usernameVariable: 'DOCKER_USERNAME',
                        passwordVariable: 'DOCKER_PASSWORD'
                    )
                ]) {
                    bat '''
                        echo %DOCKER_PASSWORD% | docker login -u %DOCKER_USERNAME% --password-stdin
                        if errorlevel 1 exit /b 1

                        docker tag springboot-k8s-demo1:1.0 %DOCKER_USERNAME%/springboot-k8s-demo1:1.0

                        docker push %DOCKER_USERNAME%/springboot-k8s-demo1:1.0
                        if errorlevel 1 exit /b 1

                        docker logout
                    '''
                }
            }
        }
    }
}