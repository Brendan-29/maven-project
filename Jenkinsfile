pipeline {
    agent any

    tools {
        maven 'Local Windows Maven'
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
        stage ('Deploy to Staging'){
           steps{
               build job: 'Deploy-To-Staging'
            }
        }
    }
} 
