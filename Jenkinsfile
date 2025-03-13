pipeline {
    agent any

    environment {
     AWS_REGION = 'us-east-1'
     IMAGE_ECR_REPO = '503561417595.dkr.ecr.us-east-1.amazonaws.com/jenkins-ci'
     ECR_REPO = '503561417595.dkr.ecr.us-east-1.amazonaws.com'
    }
    stages {
        stage ('CodeScan'){
            steps { 
                 sh 'trivy fs . -o result.html'
                 sh 'cat result.html'
           }
        }
        stage('dockerLogin'){
            steps {
                 sh "aws ecr get-login-password --region $AWS_REGION | docker login --username AWS --password-stdin 503561417595.dkr.ecr.us-east-1.amazonaws.com"

            }
        }
        stage ('dockerimagebuild'){
           steps {
             sh 'docker build -t jenkins-ci .'
        }     
} 
        stage ('dockerimagetag'){
            steps {
                sh "docker tag jenkins-ci:latest $IMAGE_ECR_REPO:latest"
                sh "docker tag jenkins-ci:latest $IMAGE_REPO:v1.$BUILD_NUMBER"
            } 
 }
        stage ('pushImage') {
            steps {
              sh "docker push $IMAGE_ECR_REPO:latest"  
              sh "docker push $IMAGE_ECR_REPO:v1.$BUILD_NUMBER"
          }
       } 
   }
}