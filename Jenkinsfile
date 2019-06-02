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
                def scannerHome = tool 'SonarQube Scanner 3.3';
                echo scannerHome;
            }
            steps{
                echo 'start SonarQube analysis';
                withSonarQubeEnv('sonarqube') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
            
        }
    }
}
