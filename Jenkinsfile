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
    stage('checkout_code'){
checkout scmGit(branches: [[name: '*/develop']], extensions: [], userRemoteConfigs: [[credentialsId: 'omer', url: 'https://github.com/omerweiner/infastracture.git']])    }

        stage('checkout_code'){
        echo "haha"
    }
}
