node {
        env.MAVEN_HOME = "${tool 'localMaven'}" 
	env.JAVA_HOME = "${tool 'localJDK'}"

        env.PATH="${env.MAVEN_HOME}/bin:${env.PATH}"
        env.PATH="${env.JAVA_HOME}/bin:${env.PATH}"

    }
      stage ('Build'){
          sh 'mvn -f pom.xml clean install deploy'
        }

    stage('SonarQube Analysis') {

                sh 'env'
		def scanner = tool "sqs3.2"
                withSonarQubeEnv('SonarQube') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
        }

