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
					archiveArtifacts artifats: '**/*.war'
				}
			}			
		}		
   }
}
