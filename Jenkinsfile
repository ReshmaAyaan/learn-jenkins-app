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
                      rm -rf node_modules package-lock.json
npm cache clean --force
                    
npm install


                    npm run build
                    ls -la
                '''
             }}
        //      stage('Test')
        // {
        //     agent {
        //         docker{
        //             image 'node:18-alpine'
        //             reuseNode true
        //         }
        //     }
        //     steps{
        //     echo "test "
        //     sh '''
        //     test -f build/index.html
        //     npm test
        //     '''
        //     }
        // }
        // stage('E2E tset')
        // {
        //      agent {
        //         docker{
        //             image 'mcr.microsoft.com/playwright:v1.39.0-jammy'
        //             reuseNode true
        //         }}
            
        //     steps{
        //     echo "test "
        //     sh '''
        //     npm install -g serve
        //     serve -s build

       
        //     npx playwright test
        //     '''
        //     }
        // }

    }
    post 
    {
        always {
             junit 'test-results/junit.xml'
 
        }
    }
}