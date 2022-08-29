def call(Map pipelineParams) {
  
  //mavensettingsconfigId=
  mavenTool = "Maven 3";
  
  def buildAndUploadSnapshot
  def buildBranch
  def isReleaseBranch
  def nextSnapshotversion
  
  
  pipeline {
    
    agent any
    
    tools {
      maven "${mavenTool}"
      jdk "zulu JDK 8"
    }
    
    parameters {
      string(defaultValue: 'NA', description: 'Release Version. e.g.1.0.0', name: 'RELEASE_VERSION', trim: true)
      booleanParam(name: 'BUILD_UPLOAD_SNAPSHOT', defaultValue: false, description: 'Do you want to build this branch and updated to SNAPSHOT?')
      
  
        stages {
            stage('checkout git') {
                steps {
                    git branch: pipelineParams.branch, credentialsId: 'GitCredentials', url: pipelineParams.scmUrl
                }
            }

            stage('build') {
                steps {
                    sh 'mvn clean package -DskipTests=true'
                }
            }
        }
    }
  }
}  
