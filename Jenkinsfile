node {    
      

      stage('Clone repository') {               
             
            checkout scm    
      }    
      stage('Build image') {         
            
            environment {
           DOCKERHUB_CREDS = credentials('dockerhub')
        }
       
            sh "docker build -t yenne1993/argocd-demo:test ."
            sh "docker login --username yenne1993 --password weLcome@#123 && docker push yenne1993/argocd-demo:test"    
       }     
      
     stage('Deploy argocd') {
      environment {
        GIT_CREDS = credentials('git')
      }
        steps {
          sh "git clone https://github.com/yenne375/argocdmanifest.git"
          sh "git config --global user.email 'jagadeesh0309@gmail.com'"

         dir("argocdmanifest") {
            sh "cd ./charts/argocd-chart && yq eval '.image.tag |= "test"' -i values.yaml"
            sh "git commit -am 'Publish new version' && git push || echo 'no changes'"
          } 

     }


   } 

} 
       
     
