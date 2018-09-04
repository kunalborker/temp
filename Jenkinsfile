pipeline {
    agent any
    tools { 
        maven 'localMaven'
          }
     def scannerHome = tool 'sqs3.2'
     stages{
     stage ('Build'){
        steps{
	      echo 'Maven Build'
              sh 'mvn -f pom.xml clean install deploy'
             }
     stage ('SonarQube'){
        steps{
              echo 'SonarQube Analysis'
	      withSonarQubeEnv {
              sh "${scannerHome}/bin/sonar-scanner"
              }
           }
        }
    
    postBuild{
         always{ 
               archive "target/**/*"
               junit 'target/surefire-reports/*.xml'
               }
             }

  notifications{
            success{
                   mail(to:"kunal.borkar@globant.com" , subject: "SUCCESS",
                                body: "Passed")
                   }
             failure{
                  mail(to:"kunal.borkar@globant.com" , subject: "SUCCESS",
                                body: "Failed")
                    }
             unstable{
                   mail(to:"kunal.borkar@globant.com" , subject: "SUCCESS",
                                body: "Unstable")
                     }
                }                  
}
