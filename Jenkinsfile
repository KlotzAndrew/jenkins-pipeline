pipeline {
    agent any
    stages {
        stage('unit tests') {
            failFast true
            parallel {
                stage('service a') {
                    steps {
                        sh 'sh service-a/test.sh'
                    }
                }
                stage('service b') {
                    steps {
                        sh 'sh service-a/test.sh'
                    }
                }
            }
        }
        stage('integration tests') {
            steps {
                sh 'sh test.sh'
            }
        }
        stage('deploy') {
            when {
              expression {
                currentBuild.result == null || currentBuild.result == 'SUCCESS'
              }
            }
            steps {
                sh 'git rev-parse HEAD'
                sh 'echo "deploying"'
            }
        }
    }
}
