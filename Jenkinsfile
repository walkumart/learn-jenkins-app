pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reusenode true
                }
            }
            steps {
                sh '''
                    ls-la
                    node --version
                    npm ci
                    npm run build
                    ls-la
                   '''
                
            }
        }
    }
}
