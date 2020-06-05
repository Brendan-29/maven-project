pipeline {
    agent any

    tools {
        maven 'Local Windows Maven'
        docker 'Local Docker Toolbox'
    }

    stages{
        stage('Build'){
            steps {
                bat "mvn clean package"
                bat "docker build . -t tomcatwebapp:${env.BUILD_ID}"
            }
        }
    }
} 
