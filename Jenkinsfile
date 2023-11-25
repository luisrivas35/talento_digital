pipeline {
    environment {
        DOCKERHUB_USERNAME = 'luisrivas35'
        DOCKERHUB_PASSWORD = credentials('DockerHub_credentials')
        DOCKERHUB_REPO = 'luisrivas35/exam-app'
    }

    agent any
    
    stages {
        stage('Checkout') {
            steps {
                script {
                    checkout scm
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    sh 'npm install'
                }
            }
        }

        stage('Build and Test') {
            steps {
                script {
                    // Add your build/test commands if applicable
                    sh 'npm test'
                }
            }
        }

        stage('Start Application') {
            steps {
                script {
                    // Start Node.js application
                    sh 'npm start'
                }
            }
        }

        stage('Dockerize') {
            steps {
                script {
                    // Build Docker image
                    sh "docker build -t $DOCKERHUB_REPO:latest ."
                    
                    // Log in to Docker Hub
                    sh "docker login -u $DOCKERHUB_USERNAME -p $DOCKERHUB_PASSWORD"
                    
                    // Push Docker image to Docker Hub
                    sh "docker push $DOCKERHUB_REPO:latest"
                }
            }
        }
    }

    post {
        always {
            // cleanWs()  // Removed workspace cleanup
        }
    }
}
