pipeline {
    agent any
    stages {
                       
                       stage('Pulling Image from ECR') {
                           steps {
 
      script{
   docker.withRegistry("https://" + "${params.ECR_IMAGE_URL}", "ecr:${params.AWS_ECR_REGION}:${params.AWS_ACCOUNT_ID}"){
     sh "docker pull ${params.ECR_IMAGE_URL}"
        }
      }
    }
                       }            

                  
                    stage("Tagging ECR Image") {
                        steps{
                        script {
                            sh "docker tag ${params.ECR_IMAGE_URL}  gcr.io/${params.GCP_PROJECT_ID}/${params.GCR_IMAGE_NAME}:${params.GCR_IMAGE_TAG}"
                            
                        }
                    }
                    }
                    stage("Pushing ECR Image to GCR") {
                        steps{
                        script {
                            withDockerRegistry([credentialsId: "gcr:${params.GCP_PROJECT_ID}", url: "https://gcr.io"]) {
                            sh "docker push gcr.io/${params.GCP_PROJECT_ID}/${params.GCR_IMAGE_NAME}:${params.GCR_IMAGE_TAG}"
                            }
                        }
                    }
                    }
                
                    
                
            
        }
    
 
}
