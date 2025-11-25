pipeline {
    agent any
    triggers {
        pollSCM('* * * * *') // fallback trigger, optional
    }
    options {
        skipDefaultCheckout true // prevent unwanted checkouts
    }
    tools {
        maven 'Maven3'
       // jdk 'JDK17'
    }

    stages {
        stage('Checkout Code') {
            when {
                branch 'main'
            }
            steps {
                git url: 'https://github.com/gangasaiusk/docker-Jenkins-learning.git', branch: 'main'
            }
        }
        stage('Build App') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t spring-boot-app:latest .'
            }
        }
        stage('Run Container') {
            steps {
                sh 'docker rm -f springboot-app || true'
                sh 'docker run -d --name springboot-app -p 8081:8080 spring-boot-app:latest'
            }
        }
    }
}
