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

        stage('SonarQube Analysis') {
            steps {
                catchError(buildResult: 'FAILURE', stageResult: 'FAILURE') {
                    script {
                        def scannerHome = tool 'SonarQube'
                        withSonarQubeEnv() {
                            sh "${scannerHome}/bin/sonar-scanner"
                        }
                    }
                }
            }
        }

        stage('Build - Code') {
            steps {
                echo "Building code now"
                sh 'mvn clean package'
                sh 'ls'
                sh "sudo docker build -t image:${env.BUILD_NUMBER} ."
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
                archiveArtifacts artifacts: "**/*.war", onlyIfSuccessful: false, allowEmptyArchive: true, 
                    caseSensitive: false, defaultExcludes: true, excludes: '',
                    include: "**/hello_world.build-number-${env.BUILD_NUMBER}.war"
            }
        }
    }
}
