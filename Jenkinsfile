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

node {
    stages{
    stage('checkout_code'){
checkout scmGit(branches: [[name: '*/develop']], extensions: [], userRemoteConfigs: [[credentialsId: 'omer', url: 'https://github.com/omerweiner/infastracture.git']])    }

        stage('Build - Code'){
        echo "Building code now"
    }

            stage('Test'){
        echo "Testing code now"
    }


            stage('Package-code'){
        echo "Package code "
    }
}
}
  
