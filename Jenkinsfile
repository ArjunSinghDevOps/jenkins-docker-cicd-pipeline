pipeline {
    agent any

    tools {
        maven 'maven'
    }

    stages {

        stage('Git Checkout') {
            steps {
                git 'https://github.com/ArjunSinghDevOps/jenkins-docker-cicd-pipeline.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t java-demo .'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker rm -f java-demo-container || true
                docker run -d --name java-demo-container -p 8081:8080 java-demo
                '''
            }
        }
    }

    post {
        success {
            echo 'Build successful'
        }
    }
}
