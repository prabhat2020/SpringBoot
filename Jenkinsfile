pipeline {
       agent any
  tools {
    maven 'Maven'
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
        
            sh "mvn sonar:sonar -Dsonar.projectKey=SpringBoot -Dsonar.host.url=http://52.143.7.186/sonarqube-1336430 -Dsonar.login=96579c2fb741c186faa0ed47b11a1fc738412e37"
        
                }
     }

  }
}
