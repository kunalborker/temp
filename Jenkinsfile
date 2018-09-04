pipeline {
  agent any
    tools { 
        maven 'localMaven' 
    }
	define {
	def scannerHome = tool 'sqs3.2'
}
    stages{
      stage ('Build'){
        steps{
	  echo 'Maven Build'
          sh 'mvn -f pom.xml clean install deploy'
        }
      }

    stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }

}
}

