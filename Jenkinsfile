pipeline {
    agent any

    stages {
        stage ('Git Install') {
            steps {                                     
					git clone "https://github.com/Sumesh1212/jenkins-example.git"
					git checkout master
            }
        }

        stage ('Sonarqube Analysis') {
            steps {                   
				environment {
					scannerHome = tool 'SonarQubeScanner'
				}
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


        stage ('Deployment Stage') {
            echo "Deploy done"
    }
	}
}
