pipeline {
    agent any
    stages {
        stage('Clean up workspace') {
            steps {
                cleanWs()
            }
        }
        stage('Build project') {
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
