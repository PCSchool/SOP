pipeline {
    agent any
    stages {
        stage('build') {
            agent { 
                docker { 
                    image 'python:3.7.2' 
                } 
            }
            steps {
                sh 'python --version'
            }
        }
        stage('build'){
            sh 'pip install -r requirements.txt'
        }
        stage('SonarQube analysis'){
            environment{
                scannerHome = '/opt/sonar-scanner-3.3.0.1492-linux'
            }
            steps{
                echo 'start SonarQube analysis';
                echo scannerHome;
                withSonarQubeEnv('sonarqube') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
            
        }
    }
}
