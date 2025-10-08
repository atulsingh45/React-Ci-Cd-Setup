pipeline {
    agent any
    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:22.12.0-alpine'
                    args '-u root'
                    reuseNode true // the node for the next stages
                }
            }

            steps {

                step('clean up workspace'){
                    cleanWs()
                }

                step('Build project') {
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
}