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
        }
    }
} 
