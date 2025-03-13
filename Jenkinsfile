pipeline {
    agent any
    stages {
        stage ('CodeScan'){
            steps { 
                 sh 'trivy --version'
           }
 }
        stage ('dockerimagebuild'){
           steps {
             sh 'docker -v'
        }     
}
        stage ('pushImage') {
            steps {
              sh 'touch text-$BUILD_ID'  
          }
       } 
   }
}