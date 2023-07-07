pipeline {
    agent any

    stages {
        stage('Clean Workspace') {
            steps {
                cleanWs()
            }
        }

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
       stage('Dockerfile-compile') {
            steps {
              sh 'terraform init'
              sh 'terraform plan -out plan -var-file=credentials.tfvars'
            }
        }


        stage('Build - Code') {
            steps {
                echo "build code"
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
                sh 'tar -czvf package-$BUILD_ID.tar.gz *'
                archive '*.tar.gz'

            }
        }
    }
}
