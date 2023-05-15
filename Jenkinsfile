  pipeline {
        agent none
        stage('SonarQube analysis') {
        steps {
            script{
            def scannerHome = tool 'sonar';
            withSonarQubeEnv('sonarqube') {
                sh "${tool("sonarscan")}/bin/sonar-scanner \
                    -Dsonar.projectKey=reactapp \
                    -Dsonar.projectName=reactapp"
            }
            }
        }
    }
      }
