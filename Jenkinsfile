node('master') {

	stage ('checkout code'){
		checkout scm
	}

	stage ('Build'){
		sh "mvn clean install"
	}

	stage ('Test Cases Execution'){
		sh "mvn clean org.jacoco:jacoco-maven-plugin:prepare-agent install -Pcoverage-per-test"
	}

	stage ('Sonar Analysis'){
		//sh 'mvn sonar:sonar -Dsonar.host.url=http://localhost:80'
	}

	stage ('Archive Artifacts'){
		archiveArtifacts artifacts: 'target/*.war'
	}

	stage ('Deployment'){
		//sh 'cp target/*.war /opt/tomcat8/webapps'
	}

	stage ('Notifications'){
		slackSend color: 'good', message: 'Message from Jenkins Pipeline'
		
		 // send to email
		  emailext (
		      subject: "STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
		      body: "Build finish"
		      to: "sctan6688@gmail.com"
		  )
	}
}
