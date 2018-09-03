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

      stage ('Unit Test') {
                steps {
                    try {
                        sh 'mvn test -Punit'
                    } catch(err) {
                        step([$class: 'JUnitResultArchiver', testResults: 
                          '**/target/surefire-reports/TEST-*UnitTest.xml'])
                        throw err
                    }
                   step([$class: 'JUnitResultArchiver', testResults: 
                     '**/target/surefire-reports/TEST-*UnitTest.xml'])
                }
            }

stage ('Integration tests') {
                steps {
                    try {
                        sh 'mvn test -Pintegration'
                    } catch(err) {
                        step([$class: 'JUnitResultArchiver', testResults: 
                          '**/target/surefire-reports/TEST-'
                            + '*IntegrationTest.xml'])
                        throw err
                    }
                    step([$class: 'JUnitResultArchiver', testResults: 
                      '**/target/surefire-reports/TEST-'
                        + '*IntegrationTest.xml'])
                }
            }
}
}
