pipeline {
    agent any
    
    environment {
        // Define the Docker Hub credentials ID
        DOCKERHUB_CREDENTIALS = 'dockerhub'
        // Define the Docker image name
        DOCKER_IMAGE = 'cristen273/cristen:sample'
        // Define the Kubernetes namespace
        //KUBE_NAMESPACE = 'your-namespace'
        // Define the Kubernetes deployment name
        KUBE_DEPLOYMENT_NAME = 'demodeployment'
    }
    
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    // Authenticate with Docker Hub
                    docker.withRegistry('https://registry.hub.docker.com', DOCKERHUB_CREDENTIALS) {
                        // Build and push the Docker image
                        def customImage = docker.build('cristen273/cristen:sample')
                        customImage.push()
                    }
                }
            }
        }
        
        stage('Deploy to Kubernetes') {
            steps {
                // Add Kubernetes deployment steps here
                withKubeConfig([credentialsID: kube-config-file]){
                    sh "kubectl apply -f deployment.yaml"
                }
            }
        }
    }
}
