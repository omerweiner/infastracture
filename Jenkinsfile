pipeline {
       stages() {
        stage('SonarQube Analysis') {
            def scannerHome = tool 'sonar';
            withSonarQubeEnv() {
            sh "${scannerHome}/bin/sonar-scanner"
            }
          }
      }
}
