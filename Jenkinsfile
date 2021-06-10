pipeline {
    agent any

    tools {
        maven "Infy'sMaven"
    }

    stages {
        stage('Checkout Git') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/subhamPr/hello-world.git'
            }
            post {
                success {
                    echo "Success!"
                }
            }
        }
        stage('Build') {
            steps {
                
                bat "mvn -Dmaven.test.failure.ignore=true clean install test package"
            }
            post {
                success {
                    echo "Success!"
                }
            }
        }
        stage('Code Quality Check') {
             steps{
                  withSonarQubeEnv('SonarQubeDefault'){
                 bat "mvn -Dmaven.test.failure.ignore=true sonar:sonar"
             }
             }
             post {
                success {
                    echo "Success!"
                }
            }
        }
}
}
