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
         stage ('Upload Artifacts') {
            steps{
                script{
	                def server = Artifactory.server('JFrog');
   	                def rtMaven = Artifactory.newMavenBuild()
                	rtMaven.tool = "Infy'sMaven"
   	                rtMaven.resolver server: server, releaseRepo: 'myNewRepo-maven-jcenter', snapshotRepo: 'myNewRepo-maven-jcenter'
   	                rtMaven.deployer server: server, releaseRepo: 'myNewRepo-libs-release-local', snapshotRepo: 'myNewRepo-libs-snapshot-local'    
   	                rtMaven.deployer.artifactDeploymentPatterns.addInclude("*.war").addExclude("*.zip")
	                def buildInfo = rtMaven.run pom: 'pom.xml', goals: 'install'
	                server.publishBuildInfo buildInfo
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
