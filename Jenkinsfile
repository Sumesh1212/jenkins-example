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
	stage('Sonar scan execution') {
            // Run the sonar scan
            steps {
                script {
                    def mvnHome = tool 'Maven 3.3.9'
                    withSonarQubeEnv {

                        sh "'${mvnHome}/bin/mvn'  verify sonar:sonar -Dintegration-tests.skip=true -Dmaven.test.failure.ignore=true"
                    }
                }
            }
        }	
}
