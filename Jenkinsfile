node('master') {
	stage ('checkout code'){
		checkout scm
	}
	
	stage ('Build'){
		sh "mvn clean install -Dmaven.test.skip=true"
	}
	
	stage ('Test Cases Execution'){
		sh "mvn clean org.jacoco:jacoco-maven-plugin:prepare-agent install -Pcoverage-per-test"
	}

	stage ('Sonar Analysis'){
		sh 'mvn sonar:sonar -Dsonar.host.url=http://localhost:9000 -Dsonar.login=535d125b6a0a56aed1db4493fff7c09b6e150e18'
	}
	stage ('Archive Artifacts'){
		archiveArtifacts artifacts: 'target/*.war'
	}
}
