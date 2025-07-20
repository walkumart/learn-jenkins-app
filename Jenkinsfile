pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    ls -la
                    npm cache clean -f
                    node --version
                    npm ci
                    npm run build
                    ls -la
                   '''
                
            }
        }

        stage('E2E') {
            agent {
                docker {
                    image 'mcr.microsoft.com/playwright:v1.39.0-jammy'
                    reuseNode true
                }
            }

            steps {
                sh '''
                    npm cache clean -f
                    npm install -g serve
                    node_module/.bin/serve -s build &
                    sleep 10
                    npx playwright test
                   '''
                
            }
        }
    }

   
}
