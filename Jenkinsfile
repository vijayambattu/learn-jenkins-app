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
                   npm ci
                   npm run build
                   ls -la
                '''
            }
        }

        stage(Test){
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }

            steps{
                echo "test Stage"
                sh '''
                    npm test
                    cd build
                    if [ -f index.html ] ; then echo "yes file exist" ; else echo "no file exists" ; fi
                    '''
            }

        }
    }

    post {
        always {
            junit 'test-results/junit.xml'
        }
    }
}