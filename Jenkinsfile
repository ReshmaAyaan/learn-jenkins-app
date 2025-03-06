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
                   
 docker run --dns 8.8.8.8 --dns 8.8.4.4 -v $(pwd):/app -w /app node:18-alpine npm install --verbose
                  


                    npm run build
                    ls -la
                '''
            }}
    }
}