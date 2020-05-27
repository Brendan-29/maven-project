pipeline {
    agent any
    
    tools {
        maven 'Local Windows Maven'
    }

    parameters {
         string(name: 'tomcat_dev', defaultValue: 'localhost:8090', description: 'Staging Server')
         string(name: 'tomcat_prod', defaultValue: 'localhost:8081', description: 'Production Server')
    }

    triggers {
         pollSCM('* * * * *')		// Polling Source Control every minute
     }

stages{
        stage('Build'){
            steps {
                bat 'mvn clean package'
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
                stage ('Deploy to Staging'){
                    steps {
                        bat "copy **/target/*.war D:\Brendans_Laptop\Tomcat\apache-tomcat-8.5.55-windows-x64\apache-tomcat-8.5.55\webapps"
                    }
                }

                stage ("Deploy to Production"){
                    steps {
                        bat "copy **/target/*.war {params.defaultValue}:/var/lib/tomcat8/webapps"
                    }
                }
            }
        }
    }
}
