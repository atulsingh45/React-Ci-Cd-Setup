pipeline {
    agent any

    environment {
        MY_VAR = 'my value'
    }

    options {
        skipDefaultCheckout(true) // Skip the default checkout
    }

    stages {

        stage('Clean up code') {
            steps {
                cleanWs()
            }
        }

        stage('Checkout using SCM') {
            steps {
                checkout scm // Checkout the code from source control
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
                timeout(time: 15, unit: 'MINUTES') {
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

        stage('Test') {
            agent {
                docker {
                    image 'node:22.12.0-alpine'
                    args '-u root'
                    reuseNode true
                }
            }
            steps {
                timeout(time: 10, unit: 'MINUTES') {
                    sh '''
                        npm run test
                    '''
                }
            }
        }

        stage('Deploy') {
            agent {
                docker {
                    image 'node:22.12.0-alpine'
                    args '-u root'
                    reuseNode true
                }
            }
            steps {
                timeout(time: 5, unit: 'MINUTES') {
                    sh '''
                        npm install -g vercel
                        echo "$MY_VAR"
                    '''
                }
            }
        }
    }
}
