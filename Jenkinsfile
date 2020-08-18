pipeline {
       agent any
  tools {
    maven 'Maven'
  }
  environment {
   registry = "prabhat2020/testing1"
   registryCredential = "06216ef3-ad77-49a6-a37b-e2e91cd08bfb"
  }
  stages {
    stage('Initialize'){
      steps{
        echo "We are doing some test"
        echo "PATH = ${PATH}"
        }
    }
    stage('Build'){
           steps
           {
        sh "mvn clean install"
    }     
    }
         stage('Sonar'){
                steps
                {
        
            sh "mvn sonar:sonar -Dsonar.projectKey=SpringPipeline -Dsonar.host.url=http://52.143.7.186/prabhat-sonarqube -Dsonar.login=0144fc0a3377b5a9fd3802be5bdf248a9b0067ae"
                }
     }
stage('Building our image') { 
             steps { 
                    script {
                 dockerImage = docker.build registry + ":$BUILD_NUMBER"
                    }
                 } 

     }
      stage('Deploy our image') { 
          steps { 
                 script { 
                  docker.withRegistry( '', registryCredential ) { 
                  dockerImage.push() 
                        }
                   } 
          }
      }
         
  
       stage('Deploy Application on K8s') {
              steps
              {
                sh("curl -LO https://storage.googleapis.com/kubernetes-release/release/\$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl")
                sh("chmod +x ./kubectl")
                sh("cat ./spring.yaml | sed s/1.0.0/${BUILD_NUMBER}/g | ./kubectl apply -f -")
                echo "Application started on port: HTTP_PORT (http)"
    }
       }
}
}
