// node {
//   stage('SCM') {
//     checkout scm
//   }
//   stage('SonarQube Analysis') {
//     def scannerHome = tool 'sonar';
//     withSonarQubeEnv() {
//       sh "${scannerHome}/bin/sonar-scanner"
//     }
//   }
// }



pipeline {
    agent any
    stages {
        stage('SCM') {
            steps {
                checkout scm
            }
        }
        stage('SonarQube Analysis'){
             steps {
              def scannerHome = tool 'sonar';
              withSonarQubeEnv() {
              sh "${scannerHome}/bin/sonar-scanner"
              }
                  }
             }        
    }
}
