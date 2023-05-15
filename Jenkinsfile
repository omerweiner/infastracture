pipeline {
agent any
stages {
 stage("Code Checkout from Github") {
  steps {
   
   //checkout the code command
  }
 }
   stage('Code Quality Check via SonarQube') {
   steps {
       node {
  stage('SCM') {
    checkout scm
  }
  stage('SonarQube Analysis') {
    def scannerHome = tool 'sonar';
    withSonarQubeEnv() {
      sh "${scannerHome}/bin/sonar-scanner"
    }
  }
}
               }
           }
       }
   }
   stage("Install Project Dependencies") {
   steps {
      
           }
       }
    
