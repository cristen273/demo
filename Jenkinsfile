pipeline {
    agent any
    
    environment {
        // Define the Docker Hub credentials ID
        DOCKERHUB_CREDENTIALS = 'dockerhub'
        // Define the Docker image name
        DOCKER_IMAGE = 'cristen273/cristen:latest'
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
                        def customImage = docker.build(DOCKER_IMAGE)
                        customImage.push()
                    }
                }
            }
        }
        
        stage('Deploy to Kubernetes'){
			steps{
				withKubeConfig([credentialsId: 'kube-config-file']) {
                              		sh "kubectl apply -f deployment.yaml"
                    }
                }
            }
        }
    }
}
