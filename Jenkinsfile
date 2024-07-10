pipeline {
    agent {
        kubernetes {
            // Define the pod template for Jenkins agent
            // Adjust memory and CPU limits as per your requirement
            yaml """
                apiVersion: v1
                kind: Pod
                metadata:
                  labels:
                    app: my-jenkins-agent
                spec:
                  containers:
                    - name: docker
                      image: docker:19.03.12
                      command:
                        - cat
                      tty: true
                    - name: kubectl
                      image: lachlanevenson/k8s-kubectl:v1.21.0
                      command:
                        - cat
                      tty: true
                  securityContext:
                    runAsUser: 0
                    fsGroup: 0
            """
        }
    }
    
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
                // Example: Use kubectl to apply your deployment.yaml file
                container('kubectl') {
                    sh "kubectl apply -f deployment.yaml"
                }
            }
        }
    }
}
