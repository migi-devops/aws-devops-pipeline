#!/usr/bin/env groovy

pipeline {   
    agent any
    stages {
        stage("test") {
            steps {
                script {
                    echo "Testing the application..."

                }
            }
        }
        stage("build") {
            steps {
                script {
                    echo "Building the application..."
                }
            }
        }

        stage("deploy") {
            steps {
                script {
                    def dockerCmd = '''
                    docker stop demo-app || true
                    docker rm demo-app || true
                    docker pull miguelprint/demo-app:1.0
                    docker run --name demo-app -p 3080:8080 -d miguelprint/demo-app:1.0
                    '''
                    sshagent(['ec2-server-key']) {
                       sh "ssh -o StrictHostKeyChecking=no ec2-user@3.8.155.161 ${dockerCmd}"
                    }
                }
            }
        }               
    }
} 
