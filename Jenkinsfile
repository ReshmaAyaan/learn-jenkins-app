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
                   # Clean up any potential corruption
                    rm -rf node_modules package-lock.json
                    npm cache clean --force
                    
                    # Install dependencies
                    npm install

                    # Ensure react-scripts is installed
                    npx react-scripts --version

                    # Build the project
                    npm run build
                    
                    npm run build
                    ls -la
                '''
            }

        }
    }
}
