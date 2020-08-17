pipeline {
       agent any
  tools {
    maven 'Maven'
  }
       environment {
        // This can be nexus3 or nexus2
        NEXUS_VERSION = "nexus3"
        // This can be http or https
        NEXUS_PROTOCOL = "http"
        // Where your Nexus is running
        NEXUS_URL = "52.143.7.186/nexuss-1336430"
        // Repository where we will upload the artifact
        NEXUS_REPOSITORY = "repository-example"
        // Jenkins credential id to authenticate to Nexus OSS
        NEXUS_CREDENTIAL_ID = "36f46d06-ecff-49e6-a230-0a2dfc1cbabc"
        registry = "raghavgeek/maven"
        registryCredential = "afd3e70c-71e8-4de3-8877-0bc4cdec3978"
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
        
            sh "mvn sonar:sonar -Dsonar.host.url=http://52.143.7.186/sonarqube-1336430 -Dsonar.login=75a228aaf0ecab50c27b819d260287d1058c87fa"
        
                }
     }
stage("Build Docker Image"){
		sh "docker build - < Dockerfile"
	}
  }
}
