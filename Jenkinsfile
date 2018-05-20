pipeline{
   agent any
   stages('Init'){
		stage('BuildTest'){
			steps{
				sh 'mvn clean package'
			}
			post{
				success{
					echo 'Now Archiving....'
					archiveArtifacts artifacts: '**/proTarget/*.war'
				}
			}			
		}
		
		stage('Deploy to Stage'){
			steps{
				build job: 'maven-project-deploy-to-stage'
			}				
		}
		
   }
}
