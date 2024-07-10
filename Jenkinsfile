pipeline {
    agent any
    
    environment {
        // Define the Docker Hub credentials ID
        DOCKERHUB_CREDENTIALS = 'docker'
        // Define the Docker image name
        DOCKER_IMAGE = 'cristen273/cristen/sample'
        // Define the Kubernetes namespace
        //KUBE_NAMESPACE = 'your-namespace'
        // Define the Kubernetes deployment name
        KUBE_DEPLOYMENT_NAME = 'your-deployment-name'
    }
    
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    // Authenticate with Docker Hub
                    docker.withRegistry('https://registry.hub.docker.com', DOCKERHUB_CREDENTIALS) {
                        // Pull the existing image if needed
                        docker.image(DOCKER_IMAGE).pull()
                        
                        // Build the Docker image (if needed)
                        docker.image('yourdockerimage:tag').build()
                        
                        // Push the Docker image to Docker Hub
                        docker.image(DOCKER_IMAGE).push()
                    }
                }
            }
        }
        
        stage('Deploy to Kubernetes') {
            steps {
                // Deploy to Kubernetes using kubectl
                container('kubectl') {
                    sh "kubectl apply -f deployment.yaml -n ${KUBE_NAMESPACE}"
                }
            }
        }
    }
}
