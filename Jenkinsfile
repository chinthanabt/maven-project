pipeline {
    agent any

    parameters {
		string(name: 'tomcat_prod', defaultValue: '34.216.225.54', description: 'Production Server')
    }

    triggers {
         pollSCM('* * * * *')
     }

	stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
	    stage ("Deploy to Production"){
            steps {
                sh "scp -i C:/Users/pc/Desktop/works/tomcat-key-pair.pem **/target/*.war ec2-user@${params.tomcat_prod}:/var/lib/tomcat8/webapps"
            }
         }
    }
}