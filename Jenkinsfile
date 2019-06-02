pipeline {
    agent { docker { image 'python:3.5.1' } }
    stages {
        stage('build') {
            steps {
                sh 'python --version'
            }
        }
        stage('SCM') {
            git 'https://github.com/foo/bar.git'
        }
        stage('SonarQube analysis') {
            // requires SonarQube Scanner 2.8+
            def scannerHome = tool 'SonarQube Scanner 2.8';
            withSonarQubeEnv('sonarscanner') {
              sh "${scannerHome}/bin/sonar-scanner"
            }
        }
    }
}

