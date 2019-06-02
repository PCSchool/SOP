pipeline {
    agent any
    stages {
        stage('build') {
            agent { 
                docker { 
                    image 'python:3.5.1' 
                } 
            }
            steps {
                sh 'python --version'
            }
        }
        stage('SonarQube analysis'){
            environment{
                scannerHome = tool 'SonarQube Scanner 3.3';
            }
            steps{
                echo 'start SonarQube analysis';
                echo ${scannerHome};
                withSonarQubeEnv('sonarqube') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
            
        }
    }
}
