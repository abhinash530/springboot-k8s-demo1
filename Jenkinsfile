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
    }
}