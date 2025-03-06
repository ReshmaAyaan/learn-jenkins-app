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
                    node --version
                    npm --version
                   rm -rf node_modules
 npm install react-scripts --save-dev


                    npm run build
                    ls -la
                '''
            }}
    }
}