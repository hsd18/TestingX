pipeline {  
    environment { 
        registry = "shashikantvermaji/java"  
        registryCredential = 'docker'  
        dockerImage = '' 
    }
    agent any 
     stages {  
        stage('Cloning our Git') { 
             steps {  
                 
                checkout([$class: 'GitSCM', branches: [[name: 'main']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '98a69b20-e09c-4c58-8654-69feb048011e', url: 'https://github.com/shashikantvermaji/test1.git']]])
            }
            
         } 
         
         
        stage('mvn clean') { 
             steps {  
                 sh 'mvn clean'
                    }
            
         } 
         stage('compile') { 
             steps {  
                 sh 'mvn compile'
                    }
            
         } 
         
         
         stage('war created') { 
             steps {  
                 sh 'mvn install'
                    }
            
         } 
         stage('Nexus artifact uplaod')
{
steps
{
nexusArtifactUploader artifacts: [[artifactId: 'java', classifier: '', file: 'target/java.war', type: 'war']], credentialsId: 'nexus', groupId: 'my', nexusUrl: '18.117.179.51:5051', nexusVersion: 'nexus3', protocol: 'http', repository: 'JavaMavenRepo', version: '0.0.1-SNAPSHOT'
}
}
          
         
 
        stage('Deploy our image') { 
             steps { 
 
            sh 'mvn tomcat7:run'
                 } 
             }
         } 
 
       

}
