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
              echo 'SOnar analysis'
              def scanner = tool "sqs3.2"
	      withSonarQubeEnv('SonarQube'){
              sh "${scanner}/bin/sonar-scanner"
              }
           }
    
    stage ('Postbuild'){
         steps{
         always{ 
               archive "target/**/*"
               junit 'target/surefire-reports/*.xml'
               }
             }
           }

    stage ('Notifications'){
         steps{
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
    }                
}
}
