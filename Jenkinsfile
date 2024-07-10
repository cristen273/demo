pipeline {
    agent {
        kubernetes {
            label 'my-label'  // Use a label to select the correct Jenkins agent pod template
            defaultContainer 'jnlp'
            yaml """
            apiVersion: v1
            kind: Pod
            metadata:
              labels:
                app: myapp
            spec:
              containers:
              - name: mycontainer
                image: myimage
              nodeSelector:
                kubernetes.io/hostname: cristen-virtualbox  // Specify the node name here
            """
        }
    }
    
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
        
        stage('Deploy to Kubernetes') {
            steps {
                // Deploy to Kubernetes using kubectl
                container('kubectl') {
                    withCredentials([kubeconfigFile(credentialsId: 'kube-config-file', variable: 'KUBECONFIG')]) {
                        sh "kubectl apply -f deployment.yaml"
                    }
                }
            }
        }
    }
}
