// node {
//   stage('SCM') {
//     checkout scm
//   }
//   stage('SonarQube Analysis') {
//     def mvn = tool 'module4';
//     withSonarQubeEnv() {
//       sh "${mvn}/bin/mvn clean verify sonar:sonar -Dsonar.projectKey=jenkins -Dsonar.projectName='jenkins'"
//     }
//   }
// }



// // Uses Declarative syntax to run commands inside a container.
// pipeline {

    agent { 
//         label 'centos7' 
    }

    triggers {
  pollSCM '* * * * *'
}
    stages {
        stage('checkout code') {
            steps {
//                 checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'github-ssh', url: 'git@github.com:lidorg-dev/hello-world-war.git']]])
            }
        }
      
      
        stage('SCM') {
            steps {
                
              
             stage('SonarQube Analysis') {
     def mvn = tool 'module4';
     withSonarQubeEnv() {
       sh "${mvn}/bin/mvn clean verify sonar:sonar -Dsonar.projectKey=jenkins -Dsonar.projectName='jenkins'"
     }
   }

            }
        }
      
      
      
        stage('Build') {
            steps {
                sh "docker build -t war:$BUILD_ID ."
            }
        }
    }
}
