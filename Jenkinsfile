pipeline {
    agent any

    tools {
        maven "Infy'sMaven"
    }

    stages {
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
