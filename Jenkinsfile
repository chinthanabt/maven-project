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
					archiveArtifacts artifacts: '**/target/*.war'
				}
			}			
		}
		
		stage('Deploy to Stage'){
			steps{
				build job: 'maven-project-deploy-to-stage'
			}				
		}

		stage ('Deploy to Production'){
            steps{
                timeout(time:5, unit:'DAYS'){
                    input message:'Approve PRODUCTION Deployment?'
                }

                build job: 'maven-project-deploy-to-prod'
            }
            post {
                success {
                    echo 'Code deployed to Production Sucessfully.'
                }

                failure {
                    echo ' Deployment failed!.'
                }
            }
        }
		
   }
}
