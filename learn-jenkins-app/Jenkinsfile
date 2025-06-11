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
    }
}