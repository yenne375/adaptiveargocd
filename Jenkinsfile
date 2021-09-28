node () {    
      

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
      
          sh "rm -rf argocdmanifest"
          sh "git clone https://github.com/yenne375/argocdmanifest.git"
          sh '''git config user.name "yenne375"'''
          sh "git config --global user.email 'jagadeesh0309@gmail.com'"

         dir("argocdmanifest") {
            sh '''
            git config --global user.email 'jagadeesh0309@gmail.com'
            cd ./charts/argocd-chart && yq eval '.image.tag |= "testnow12"' -i values.yaml

             cd ../../ && pwd && users && git commit -am 'Publish new version' && git push https://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:x-oauth-basic@@github.com:yenne375/argocdmanifest.git || echo 'no changes'
              
              '''
          } 

     


   } 

} 
       
     
