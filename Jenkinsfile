pipeline {
    agent any
    
    environment {
        DOCKER_IMAGE = 'your-docker-username/tip-calculator-app'
        DOCKER_REGISTRY = 'docker.io'  // Use the appropriate registry (e.g., Docker Hub)
    }
    
    stages {
        stage('Checkout') {
            steps {
                // Get the code from GitHub
                checkout scm
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image using the Dockerfile
                    sh 'docker build -t $DOCKER_IMAGE .'
                }
            }
        }
        
        stage('Push to Docker Hub') {
            steps {
                script {
                    // Login to Docker Hub (replace with your credentials)
                    sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'
                    sh 'docker push $DOCKER_IMAGE'
                }
            }
        }
        
        stage('Deploy') {
            steps {
                script {
                    // Run the container with Docker Compose
                    sh 'docker-compose up -d'
                }
            }
        }
    }
    
    post {
        always {
            // Clean up after the job (optional)
            sh 'docker system prune -f'
        }
    }
}
