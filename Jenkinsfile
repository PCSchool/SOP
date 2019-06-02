pipeline {
    agent { docker { image 'python:3.5.1' } }
    stages {
        stage('build') {
            steps {
                sh 'python --version'
            }
        }
    }
}
node{
        stage('SCM') {
            git 'https://github.com/PCSchool/SOP.git'
        }
        stage('SonarQube analysis') {
            // requires SonarQube Scanner 2.8+
            def scannerHome = tool 'SonarQube Scanner 2.8';
            withSonarQubeEnv('sonarscanner') {
              sh "${scannerHome}/bin/sonar-scanner"
            }
        }
    }
