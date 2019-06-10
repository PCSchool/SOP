/*pipeline {
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
}*/
node {
    def app

    environment {
        registry = "pcschool/sop"
        registryCredential = 'dockerhub'
        dockerImage = ''
        scannerHome = '/opt/sonar-scanner-3.3.0.1492-linux'
    }
    withMaven(maven:'maven') {
        stage('Build docker') {
            echo 'Build docker image'
            dir ('jenkins-service') {
                app = docker.build "localhost:5000/jenkins-service:${env.version}"
                app.push()
            }
        }

        stage ('Test docker image') {
            echo 'Test docker image'
            docker.image("localhost:5000/jenkins-service:${env.version}").run('-p 2222:2222 -h account --name account --link discovery')
        }

        stage('SonarQube analysis'){
            steps{
                echo 'start SonarQube analysis';
                echo scannerHome;
                withSonarQubeEnv('sonarqube') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }

        stage ('Deployment docker') {
            steps {
                    echo 'Publish docker'
                    // push docker naar docker hub
                    sh 'docker login -u pcschool -p P@ssw0rd'
                    docker.withRegistery('https://registry.hub.docker.com', 'pcschool') {
                        app.push('${env.BUILD_NUMBER}')
                        app.push('otap')
                    }
            }
            //build job: 'jenkins', wait: false
        }     

    }

}
