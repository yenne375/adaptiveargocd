node {    
      

      stage('Clone repository') {               
             
            checkout scm    
      }    
      stage('Build image') {         
            
            environment {
           DOCKERHUB_CREDS = credentials('dockerhub')
        }
       
            sh "docker build -t yenne1993/argocd-demo:${env.GIT_COMMIT} ."
            sh "docker login --username $DOCKERHUB_CREDS_USR --password $DOCKERHUB_CREDS_PSW && docker push yenne1993/argocd-demo:${env.GIT_COMMIT}"    
       }     
      
      


   }  
       
     
