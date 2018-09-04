pipeline {
    agent any
    tools { 
        maven 'localMaven'
          }
     stages{
     stage ('Build'){
        steps{
	      echo 'Maven Build'
              sh 'mvn -f pom.xml clean install deploy'
             }
          }
     stage ('SonarQube'){
          steps{
              sh 'mvn sonar:sonar -Dsonar.host.url=http://127.0.0.1:9000/sonar'
              }
           }
    }                
}
