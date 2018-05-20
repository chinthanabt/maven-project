pipeline {
    agent any

    parameters {
		string(name: 'tomcat_prod', defaultValue: '35.164.26.78', description: 'Production Server')
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

        stage ('Deployments'){
            parallel{
                stage ("Deploy to Production"){
                    steps {
                        sh "scp -i C:\Users\pc\Desktop\works\Tomcat_Maven_Project.pem **/target/*.war ec2-user@${params.tomcat_prod}:/var/lib/tomcat8/webapps"
                    }
                }
            }
        }
    }
}