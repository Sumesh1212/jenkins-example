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
        		userRemoteConfigs: [[credentialsId: 'GitHub_Token', url: "https://github.com/Sumesh1212/jenkins-example.git"]]]
            }
        }

        stage ('Sonarqube Analysis') {
            steps {
		    steps {
			    withSonarQubeEnv('SonarQube',envOnly: true) {
				     sh "export PATH=/opt/sonar-scanner/bin:$PATH ; \
				    sonar-scanner \
				    -Dsonar.projectName="jenkins-example" \
				    -Dsonar.projectKey="Sample:7899756022" \
				    -Dsonar.sources=${sonarProperties.projectName} \				    
				    -Dsonar.projectVersion="1.0" \
				    -Dsonar.branch.name="master" \				    
			    }
			    timeout(time: 10, unit: 'MINUTES') {
				    waitForQualityGate abortPipeline: true
			    }
		    }
	    }
	}
    }
}
