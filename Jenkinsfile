pipeline {
  agent any
  tools { 
        maven 'Maven_3_5_2'  
    }
   environment {
        SONAR_TOKEN = credentials('SONAR_TOKEN')
    }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {	
             sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=buggywebapps -Dsonar.organization=buggywebapps -Dsonar.host.url=https://sonarcloud.io -Dsonar.token=93f470b908a46156f5844'			}
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
