pipeline {
  agent any
  tools { 
        maven 'Maven_3.2.5"  
    }
   environment {
        SONAR_TOKEN = credentials('SONAR_TOKEN')
    }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {	
             sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=buggywebapps -Dsonar.organization=buggywebapps -Dsonar.host.url=https://sonarcloud.io -Dsonar.token=$SONAR_TOKEN'			}
    }

	stage('RunSCAAnalysisUsingSnyk') {
            steps {		
				withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
					sh 'mvn snyk:test -fn'
				}
			}
    }		
  }
}
