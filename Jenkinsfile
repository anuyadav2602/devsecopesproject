pipeline {
  agent any
  tools { 
        maven 'maven_3_8_4'  
    }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=asgbuggywebapp02 -Dsonar.organization=asgbuggywebapp02 -Dsonar.host.url=https://sonarcloud.io -Dsonar.token=edf2b50c531961bc526d3ee65d8c9e735fa89371'
			}
    }

	
  }
}




###





