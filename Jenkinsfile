
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
       stage('Docker-container deployment') {
            steps {
              sh 'docker images'
              sh 'docker run -itd --name jenkins.$BUILD_ID  -p 8088:8088 module7_jenkins'

            }
        }


 

        stage('Docker container Test') {
            steps {
              sh 'docker ps -a'
              sh 'docker logs jenkins.$BUILD_ID'
              sh 'docker inspect jenkins.$BUILD_ID'
              sh 'docker stop jenkins.$BUILD_ID'
              sh 'docker rm jenkins.$BUILD_ID'
            }
        }
        stage('Push Docker Image') {
        steps {
            script {
                // Tag the Docker image
                def imageTag = "127.0.0.1:8084/docker_private/module7_jenkins:$BUILD_ID"
                sh "docker tag module7_jenkins:$BUILD_ID ${imageTag}"
    
                // Log in to Nexus Artifactory
                sh "docker login 127.0.0.1:8084 -u admin -p 1111"
    
                // Push the Docker image to Nexus Artifactory
                sh "docker push ${imageTag}"
            }
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
