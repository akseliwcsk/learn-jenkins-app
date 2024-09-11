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
        stage('Test') {
        agent {
                docker {
                    image 'node:19-bullseye'
                    reuseNode true
                }
            }
        steps {
                sh '''
                echo "Test stage"
                stat build/index.html
                npm test a
                '''
            }
        }

        post {
            always {
                junit "test-results/junit.xml"
            }
        }
    }
}
