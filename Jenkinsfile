import jenkins.model.*
jenkins = Jenkins.instance
pipeline {
    agent any
	stage ('Git Install') {
		    steps {                                     
			checkout changelog: false, 
				poll: false, 
				scm: [$class: 'GitSCM', branches: [[name: pipelineBranch]], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], 
				userRemoteConfigs: [[credentialsId: 'GitHub_Token', url: "https://github.com/Sumesh1212/jenkins-example.git"]]]
		    }
		}
	stage('SonarQube Analysis') {
		def mvn = tool 'Default Maven';
		withSonarQubeEnv() {
			sh "${mvn}/bin/mvn clean verify sonar:sonar -Dsonar.projectKey=Sample:7899756022"
		}
	}	
}
