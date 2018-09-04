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
              def scanner = tool "sqs3.2"
	      withSonarQubeEnv('SonarQube'){
              sh "${scanner}/bin/sonar-scanner"
           }
    
    stage ('Postbuild'){
         always{ 
               archive "target/**/*"
               junit 'target/surefire-reports/*.xml'
               }
             }

    stage ('Notifications'){
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
