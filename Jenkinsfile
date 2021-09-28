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
          sh "git clone https://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@github.com:yenne375/argocdmanifest.git"
          sh "git config --global user.email 'jagadeesh0309@gmail.com'"

         dir("argocdmanifest") {
            sh '''
            git config --global user.email 'jagadeesh0309@gmail.com'
            cd ./charts/argocd-chart && yq eval '.image.tag |= "test"' -i values.yaml

             cd ../../ && git commit -am 'Publish new version' && git push || echo 'no changes'
              
              '''
          } 

     


   } 

} 
       
     
