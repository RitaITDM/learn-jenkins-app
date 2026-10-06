pipeline {
    agent{
     docker {
        image 'node:18-alpine'
         reuseNode true 
    }
    }

    enviroment{
        NETLIFY_SITE_ID = '3c556d46-04f8-42dd-9b55-15a65e9dc567'
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
                  npx netlify-cli --version
                  echo "Deploying to production. Site ID : $NETLIFY_SITE_ID"
                '''
            }
        }
    }
}
