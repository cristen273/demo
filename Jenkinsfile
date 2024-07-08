pipeline{

 agent any

 environment {
  DOCKERHUB_CREDENTIALS=credentials('dockerhub')
 }

 stages {
  stage('Build') {

   steps {
    echo 'build'
   }
  }

  stage('Login') {

   steps {
    echo 'login'
   }
  }

  stage('Push') {

   steps {
    echo 'push'
   }
  }

  stage('Deploy to Kubernetes'){
   steps{
    echo 'kube deployed'
   }
  } 
 }
}
