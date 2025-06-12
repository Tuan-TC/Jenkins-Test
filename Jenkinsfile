pipeline {
    agent any
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