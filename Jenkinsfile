pipeline {
    agent any
    tools {
        maven 'maven_3_9_3'
    }
    stages {
        stage('Build Maven Project') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/harshapadidala/devops-automation']])
                sh 'mvn clean install'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t 015245199/message-server:latest .'
                }
            }
        }
        stage('Push Image to DockerHub') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'dockerhubpwd', variable: 'dockerhubpwd')]) {
                        sh 'docker login -u 015245199 -p ${dockerhubpwd}'
                    }
                    sh 'docker push 015245199/message-server:latest'
                }
            }
        }
    }
}