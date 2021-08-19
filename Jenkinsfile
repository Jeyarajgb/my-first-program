pipeline {

  agent any
  
  environment{
      workerType = 'MICRO'
      cloudhub = credentials('cloudhub_credential')
      region= 'us-east-2'
        NEXUS_VERSION = "nexus3"
        NEXUS_PROTOCOL = "http"
        NEXUS_URL = "127.0.0.1:8081"
        NEXUS_REPOSITORY = "maven-nexus-repo"
        NEXUS_CREDENTIAL_ID = "nexus-user-credentials"
  }
  
  stages{
  
     
    stage('Build') {
    
      steps{
      
        echo "selected branch: ${Branch}" 
      
        bat "mvn clean package install"
      }
    }
    
  }    
  
 
}