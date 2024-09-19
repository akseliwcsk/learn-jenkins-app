pipeline {
    agent {
        label 'jenkins_slave' // Ensure this label matches your Jenkins slave node label
    }
    stages {
        stage('Build') {
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
            steps {
                sh '''
                    echo "Test stage"
                    stat build/index.html
                    npm test a
                '''
            }
        }
        stage('E2E') {
            steps {
                sh '''
                    npm install serve
                    node_modules/.bin/serve -s build &
                    sleep 10
                    npx playwright test --reporter=html
                '''
            }
        }
    }
    post {
        always {
            junit "jest-results/junit.xml"
        }
    }
}
