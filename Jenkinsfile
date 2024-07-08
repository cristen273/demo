pipeline{

 agent any

 environment {
  DOCKERHUB_CREDENTIALS=credentials('dockerhub')
 }

 stages {
  stage('Build') {

   steps {
    sh 'docker build -t cristen273/cristen:jenkinsdemo .'
   }
  }

  stage('Login') {

   steps {
    sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
   }
  }

  stage('Push') {

   steps {
    sh 'docker push cristen273/cristen:jenkinsdemo'
   }
  }

  stage('Deploy to Kubernetes'){
   steps{
    withKubeConfig([credentialsId: 'Kube-config-k8s']) {
     sh 'kubectl apply -f deployment.yaml'
    }
   }
  } 
 }
}
