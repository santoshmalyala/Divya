pipeline{
    agent any
    triggers
    {
        pollSCM " * * * * * "
    }
    
        options
    {
        buildDiscarder(logRotator(numToKeepStr: '5' , daysToKeepStr: '5'))
        timeout(time: 1, unit: 'HOURS')
    }
    tools
    {
        maven 'maven'
        jdk 'java'
    }
    stages
    {
         stage('Checkout')
        {
          
            steps
            {
                git 'https://github.com/santoshmalyala/Divya.git'
            }
        }
        
        stage('Build')
        {
            
            steps
            {
                bat 'mvn clean compile package'
            }
        }
        stage('Sonar')
        {
           
            steps
            {
                withSonarQubeEnv(installationName: 'sonar')
                {
                    bat 'mvn sonar:sonar'
                }
            }    
        }       

    }
}        
    {
        buildDiscarder(logRotator(numToKeepStr: '5' , daysToKeepStr: '5'))
        timeout(time: 1, unit: 'HOURS')
    }
    tools
    {
        maven 'maven'
        jdk 'java'
    }
    environment {
        NEXUS_VERSION = "nexus3"
        NEXUS_PROTOCOL = "http"
        NEXUS_URL = "localhost:8081"
        NEXUS_REPOSITORY = "divya890"
        NEXUS_CREDENTIAL_ID = "NEXUS_CRED"
    }
    stages
    {
         stage('Checkout')
        {
          
            steps
            {
                git 'https://github.com/santoshmalyala/Divya.git'
            }
        }
        
        stage('Build')
        {
            
            steps
            {
                bat 'mvn clean compile package'
            }
        }
        stage('Sonar')
        {
           
            steps
            {
                withSonarQubeEnv(installationName: 'sonar')
                {
                    bat 'mvn sonar:sonar'
                }
            }    
        } 

        stage('Nexus'){
            steps{
              nexusArtifactUploader artifacts: [[artifactId: 'spring-petclinic', classifier: '', file: 'target\\petclinic.war', type: 'war']], credentialsId: '22a6cbfe-f0f8-4945-aa14-ba17a5e2f56d', groupId: 'spring-petclinic', nexusUrl: 'http://localhost:8081/', nexusVersion: 'nexus3', protocol: 'http', repository: 'http://localhost:8081/repository/Devops/', version: '4.2.5'
        }
              
              

    }
}  

}
