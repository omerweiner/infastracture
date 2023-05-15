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



pipeline {
    agent any
    stages {
        stage('checkout_code') {
           echo "hahaha"
        }
        stage('test'){
            
                 echo "ha22222222"
            
        }
    }
}
