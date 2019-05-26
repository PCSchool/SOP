pipeline {
    agent any
        stages {
            stage('start') {
                steps {
                    echo 'hello jenkins'
                }
            }
            stage('build'){
                agent { docker {image 'ubuntu'}}
            }
        }
}