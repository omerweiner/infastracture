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
        echo "haha"
    }
}
