pipeline {

  agent any
  
  environment{
      workerType = 'MICRO'
      unique_Id = UUID.randomUUID().toString()
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
     when {
        expression {
            return ( params.Action == 'Build' || params.Action == 'Build_Deploy') 
        }
     }
    
      steps{
      
        echo "selected branch: ${params.Git_Branch}" 
      
        bat "mvn clean package install"
      }
    }
    
    
     stage('Deploy') {
     when {
        expression {
            return (params.Action == 'Build_Deploy') 
        }
     }
    
      steps{
      
        echo "Selected, Build_Deploy" 
       
      }
    }
    
  }
 }