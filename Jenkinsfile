pipeline {
    agent any
    
        environment
        {
         NETLIFY_SITE_CODE='fc3f6e81-5609-4623-8577-f98e90d35250'
         NETLIFY_AUTH_TOKEN=credential('netlify-token')
        }
    

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
               npm install


                    npm run build
                    ls -la
                '''
             }}
        stage('Test')
        {
            parallel
        {
            stage('UnitTest')
             {
             agent {
               docker{
                   image 'node:18-alpine'
                   reuseNode true
                     }
                    }
            steps{
            echo "test "
             sh '''
            test -f build/index.html
            npm test
            '''
              }
               post 
     {
         always {
              junit 'jest-results/junit.xml'
             
        }
            }
             }

            stage('E2E tset')
            {
               agent {
               docker{
                   image 'mcr.microsoft.com/playwright:v1.39.0-jammy'
                  reuseNode true
                }}
            
             steps{
            echo "test "
            sh '''
            npm install serve
                    node_modules/.bin/serve -s build &
                    sleep 10
                    npx playwright test --reporter=html  
             '''
            }
             post 
     {
         always {
             
              publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, icon: '', keepAll: false, reportDir: 'playwright-report', reportFiles: 'index.html', reportName: 'playwright-HTML Report', reportTitles: '', useWrapperFileDirectly: true])
 
        }
         }
         
            }
        }
             
        

    }
    stage('Deploy') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    npm install netlify-cli
                    node_modules/.bin/netlify --version
                    echo "deployesited_id :$NETLIFY_SITE_CODE"
                    node_modules/.bin/netlify status
                '''
            }
        }

   
    
}
}