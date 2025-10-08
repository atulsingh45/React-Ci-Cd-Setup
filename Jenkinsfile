pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Clean up workspace') {
            steps {
                cleanWs()
            }
        }

        stage('Check workspace contents') {
            steps {
                sh 'ls -la'
            }
        }

        stage('Build project') {
            agent {
                docker {
                    image 'node:22.12.0-alpine'
                    args '-u root'
                }
            }
            environment {
                WORKSPACE_DIR = "${pwd()}"
            }
            steps {
                // Explicitly mount current directory and set working directory
                script {
                    def currentDir = pwd()
                }
                // Run commands in Docker with volume mounted
                container('node:22.12.0-alpine') {
                    sh '''
                        ls -la
                        node --version
                        npm --version
                        npm install
                        npm run build
                        ls -la
                    '''
                }
            }
        }
    }
}
