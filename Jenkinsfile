pipeline {
  agent any
  stages {
    stage('SCM') {
     steps {
      checkout scm
     }
        }
        stage('SonarQube analysis') {
         steps {
            script {
            // requires SonarQube Scanner 2.8+
            scannerHome = tool 'sonar'
            }
            withSonarQubeEnv('SonarQube Scanner') {
            sh "${scannerHome}/bin/sonar-scanner"
            }
               }
        }
  }
}
