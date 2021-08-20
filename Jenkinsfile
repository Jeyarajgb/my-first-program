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
      
        steps {
        
        echo "mule version ${params.MuleVersion}"
        echo "environment ${params.Environment}"
        echo "business group ${params.Business_Domain}"
        echo "objectStoreV2 ${params.objectStoreV2}"
        echo "Application Name ${params.Application_Name}"
        echo "Workers Size ${params.WorkersSize}"
        echo "userid ${cloudhub_USR}"
        echo "pwd ${cloudhub_PSW}"
        
        bat "mvn package mule:deploy -Dmule.version=${params.MuleVersion} -Dcloudhub.application.name=${params.Application_Name} -Dcloudhub.env=${params.Environment} -Dcloudhub.works.size=${params.WorkersSize} -Dcloudhub.region=${region} -Dcloudhub.worker.type=${workerType} -Dcloudhub.username=${cloudhub_USR} -Dcloudhub.password=${cloudhub_PSW}"
     }
       
      }
    }
    
  }
 }