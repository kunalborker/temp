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


stage('Tests') {
        try {
                sh 'mvn clean test'
        } finally {
            junit testResults: 'target/test-classes/*.xml', allowEmptyResults: true
            archiveArtifacts 'target/test-classes/**'
                }
         }
}
}
