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

        stage ('Sonarqube Analysis') {		 
		def scannerhome = tool 'Sonar-Scanner';
		withSonarQubeEnv('SonarQube') {
			sh """${scannerhome}/bin/sonar-runner -D sonar.login = admin -D sonar.password = Sumesh@1294 """
		}
		timeout(time: 10, unit: 'MINUTES') {
			waitForQualityGate abortPipeline: true
		}	
	}    
}
