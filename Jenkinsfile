pipeline {
    agent { docker {image 'python:2.7-slim'} }
    stages {
        stage('start') {
            steps {
                sh 'python --version'
            }
        }
    }
}