pipeline {
    agent any
    environment {
        NETLIFY_AUTH_TOKEN = credentials('netlify')
        NETLIFY_SITE_ID = '52cf3f8c-e2e8-4079-b85e-ca653ed49794'
    }
    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:21-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                cd learn-jenkins-app
                yarn -v
                yarn
                yarn build
                '''
            }
        }
        stage('Test') {
            agent {
                docker {
                    image 'node:21-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                cd learn-jenkins-app
                test -f build/index.html
                yarn test
                '''
            }
        }
        stage('Deploy') {
            agent {
                docker {
                    image 'node:21-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                npm install netlify-cli
                node_modules/.bin/netlify --version
                echo "Thay doi id $NETLIFY_SITE_ID"
                node_modules/.bin/netlify status
                
                '''
            }
        }
    }
    post {
        always {
            junit 'learn-jenkins-app/test-results/junit.xml'
        }
    }
}