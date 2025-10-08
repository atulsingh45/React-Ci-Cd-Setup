pipeline {
    agent any
    options {
        skipDefaultCheckout(true)
    }
    stages {

        stage ('clean up code') {
            steps {
                cleanWs()
            }
        }

        stage('Checkout using SCM') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            agent {
                docker {
                    image 'node:22.12.0-alpine'
                    args '-u root'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    ls -l
                    node --version
                    npm --version
                    npm install
                    npm run build
                    ls -l
                '''
            }
        }
    }
}
