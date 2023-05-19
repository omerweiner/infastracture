pipeline {
    agent any

    stages {
        stage('checkout_code') {
            steps {
                checkout scmGit(
                    branches: [[name: '*/develop']],
                    extensions: [],
                    userRemoteConfigs: [[credentialsId: 'omer', url: 'https://github.com/omerweiner/infastracture.git']]
                )
            }
        }

        stage('SCM') {
            steps {
                checkout scm
            }
        }

        stage('SonarQube Analysis') {
            steps {
                script {
                    def scannerHome = tool 'SonarQube'
                    withSonarQubeEnv() {
                        sh "${scannerHome}/bin/sonar-scanner"
                    }
                }
            }
        }

        stage('Build - Code') {
            steps {
                echo "Building code now"
                sh 'mvn clean package'
                sh 'ls'
                sh 'echo "${env.BUILD_NUMBER}"'
                sh 'sudo docker build -t image.${env.BUILD_NUMBER}'
                sh 'sudo docker images'

            }
        }

        stage('Test') {
            steps {
                echo "Testing code now"
            }
        }

        stage('Package-code') {
            steps {
                echo "Package code"
            }
        }
    }
}
