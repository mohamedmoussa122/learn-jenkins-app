pipeline {
    agent any

    stages {
        stage('docker') {
            agent {
                docker {
                    image 'node:23-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    ls -la
                    node -v
                    npm -v
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }

        stage('test')  {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    test -f build/index.html
                    npm test
                    '''
            }
        }
    }

    // post {
    //     always {
    //         junit './test-results/junit.xml'
    //     }
    // }
}
