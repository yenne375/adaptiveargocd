def prevcom = 'initial_value'
node () {    
      

      stage('Clone repository') {               
             
            checkout scm    
      }    
      stage('Build image') {         
            
            environment {
           DOCKERHUB_CREDS = credentials('dockerhub')
        }
       
            sh "docker build -t yenne1993/argocd-demo:\$(git rev-parse --short HEAD) ."
            sh "docker login --username yenne1993 --password weLcome@#123 && docker push yenne1993/argocd-demo:\$(git rev-parse --short HEAD)" 
            sh "export prevcom=\$(git rev-parse --short HEAD)"   
       }     
      
     stage('Deploy argocd') {
      
          sh "rm -rf argocdmanifest"
          sh "git clone https://github.com/yenne375/argocdmanifest.git"
          sh '''git config user.name "yenne375"'''
          sh "git config --global user.email 'jagadeesh0309@gmail.com'"

         dir("argocdmanifest") {
            sh '''
            git config --global user.email 'jagadeesh0309@gmail.com'
            export com=$(git rev-parse --short HEAD) 
            echo $com
            cd ./charts/argocd-chart 
            
            
            yq eval '.image.tag |= "'${prevcom}'"'  values.yaml | tee test403.yaml
            
            cat test403.yaml > values.yaml
            

             cd ../../ && pwd && users && git commit -am 'Publish new version' && git push git@github.com:yenne375/argocdmanifest.git || echo 'no changes'
              
              '''
          } 

     


   } 

} 
       
     
