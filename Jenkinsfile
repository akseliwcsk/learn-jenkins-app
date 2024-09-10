pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:19-bullseye'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }
        stage('Test'){
            steps { sh 'echo "Test stage"'
        }
    }
}
