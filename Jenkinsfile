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
    }
    post {
        always {
            junit 'learn-jenkins-app/test-results/junit.xml'
        }
    }
}