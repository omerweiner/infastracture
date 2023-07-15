
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
                script {
                    // Retrieve the public IP address using the script
                    def publicIp = sh(returnStdout: true, script: 'curl -s https://api.ipify.org').trim()

                    // Set the IP address as an environment variable
                    env.MY_IP = publicIp

                    // Optional: Print the IP address for verification
                    echo "My IP address is: $publicIp"
                }
                
             // sh 'public_ip=$(curl -s https://api.ipify.org)'
              //sh 'export MY_IP="$public_ip"'
              sh 'docker images'
              sh 'docker run -itd --name jenkins.$BUILD_ID  -p 8088:8088 module7_jenkins'
              sh 'docker ps -a'
              //sh 'curl http:/$public_ip:8088/hello-world-war-1.0.0/ '
              sh 'docker stop jenkins.$BUILD_ID'
              sh 'docker rm jenkins.$BUILD_ID'
            

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
