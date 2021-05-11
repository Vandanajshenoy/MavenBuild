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
		sh 'mvn sonar:sonar -Dsonar.host.url=http://localhost:9000 -Dsonar.login=fe8669f735f1dc8807adff3f5ed4e21273d2f016'
	}
	stage ('Archive Artifacts'){
		archiveArtifacts artifacts: 'target/*.war'
	}
}
