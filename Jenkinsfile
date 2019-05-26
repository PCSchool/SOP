pipeline {
         agent any
         stages {
                 stage('One') {
                 steps {
                     echo 'Hello Jenkins'
                 }
                 }
                 stage('build'){
                     steps {
                         echo 'build'
                     }
                 }
                 stage('Test') {
                 parallel { 
                            stage('Unit Test') {
                           steps {
                                echo "Running the unit test..."
                           }
                           }
                            stage('Integration test') {
                              agent {
                                    docker {
                                            reuseNode true
                                            image 'ubuntu'
                                           }
                                    }
                              steps {
                                echo "Running the integration test..."
                              }
                           }
                           }
                           }
              }
}