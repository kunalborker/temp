node {
        env.MAVEN_HOME = "${tool 'localMaven'}" 
	env.JAVA_HOME = "${tool 'localJDK'}"
        env.SONAR_HOME = "${tool 'sqs3.2'}"

        env.PATH="${env.MAVEN_HOME}/bin:${env.PATH}"
        env.PATH="${env.JAVA_HOME}/bin:${env.PATH}"
        env.PATH="${env.SONAR_HOME}/bin:${env.PATH}"

    }
      stage ('Build'){
          sh 'mvn -f pom.xml clean install deploy'
        }

    stage('SonarQube Analysis') {

                sh 'env'
                withSonarQubeEnv('SonarQube') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
        }

