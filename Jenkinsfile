pipeline {
    agent{
     docker {
        image 'node:18-alpine'
         reuseNode true 
    }
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

        stage('Test'){
            steps{
                sh '''
                test -f build/index.html
                npm test
                '''
            }
        }

                stage('Deploy') {
            steps {
                sh '''
                  npm install netlify-cli -g
                  node_modules/.bin/netlify --version
                '''
            }
        }
    }
}
