pipeline {
    agent any
    environment {
  buildNumber = "BUILD_NUMBER"
                }

    stages {
        stage('checkout_code') {
            steps {
                git branch: 'dev', credentialsId: 'Git_cred_Muzammil', url: 'https://github.com/quadrimuzammil/k8s-hello-node.git'
                  }
                               }
        /*stage('build_package') {
            steps {
                sh 'pwd'
             dir("backend") {    
                sh "npm install"
                            }
                  }
                               } */
        
    stage('Build_docker_image') {
            steps {
            
                sh 'docker build -t 033385524530.dkr.ecr.ap-south-1.amazonaws.com/backend-demo:Latest . '
                           
                  }
                                }    
  stage('Push_Imgae_ECR') {
            steps {
            
// This step should not normally be used in your script. Consult the inline help for details.
withDockerRegistry(credentialsId: 'ecr:ap-south-1:aws_credentials_for_ecr', url: 'https://033385524530.dkr.ecr.ap-south-1.amazonaws.com/backend-demo')
                                {
     sh 'docker push 033385524530.dkr.ecr.ap-south-1.amazonaws.com/backend-demo:Latest'
                                  }
                
               
                
            
                  }
                            }
        stage('Deploy to Eks'){
            steps{
                    dir("kubernetes") { 
                    sh "kubectl apply -f deployment.yaml"
                                  }
                 }
                              }
 
  
    }
}
