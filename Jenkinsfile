pipeline {
  agent any
  tools { 
        maven 'maven_3_8_4'  
    }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=asgbuggywebapp02 -Dsonar.organization=asgbuggywebapp02 -Dsonar.host.url=https://sonarcloud.io -Dsonar.token=2388aa5baea5429196c0a312175219ef76b03a7a'
			}
    }
	
	stage('RunSCAAnalysisUsingSnyk') {
            steps {		
				withCredentials([string(credentialsId: 'snyk_token', variable: 'synk_token')]) {
					sh 'mvn snyk:test -fn'
				}
			}
    }
	stage('Build') { 
            steps { 
               withDockerRegistry([credentialsId: "dockerlogin", url: "http://3.107.10.94:8081/manage/credentials/store/system/domain/_/credential/dockerlogin"]) {
                 script{
                 app =  docker.build("asg")
                 }
               }
            }
    }

	stage('Push') {
            steps {
                script{
                    docker.withRegistry('https://ap-southeast-2.console.aws.amazon.com/ecr/private-registry/repositories?region=ap-southeast-2:aws-credentials') {
                    app.push("latest")
                    }
                }
            }
    	}

   }
}


	
  











