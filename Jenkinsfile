import jenkins.model.*
jenkins = Jenkins.instance
pipeline {
    agent any

    stages {
        stage ('Git Install') {
            steps {                                     
		checkout changelog: false, 
        		poll: false, 
        		scm: [$class: 'GitSCM', branches: [[name: pipelineBranch]], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], 
        		userRemoteConfigs: [[credentialsId: 'GitHub', url: "https://github.com/Sumesh1212/jenkins-example.git"]]]
            }
        }

        stage ('Sonarqube Analysis') {
            steps {
		    steps {
			    withSonarQubeEnv('sonarqube') {
				    sh "${scannerHome}/bin/sonar-scanner"
			    }
			    timeout(time: 10, unit: 'MINUTES') {
				    waitForQualityGate abortPipeline: true
			    }
		    }
	    }
	}
    }
}
