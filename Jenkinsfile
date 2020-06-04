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
                stage ('Deploy to Staging Tomcat'){
                    steps {
                        bat "copy **/target/*.war D:\\Brendans_Laptop\\Tomcat\\apache-tomcat-8.5.55-windows-x64\\apache-tomcat-8.5.55\\webapps\\"
                    }
                }

                stage ('Deploy to Production Tomcat'){
                    steps {
                        bat "copy **/target/*.war D:\\Brendans_Laptop\\Tomcat\\apache-tomcat-8.5.55-windows-x64\\Tomcat_prod_instance\\webapps\\"
                    }
                }
            }
        }
    }
}
