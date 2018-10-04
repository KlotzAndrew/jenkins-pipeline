pipeline {
    agent any
    stages {
        stage('unit tests') {
            failFast true
            parallel {
                stage('service a') {
                    steps {
                        dir("service-a") {
                            sh 'sh test.sh'
                        }
                    }
                }
                stage('service b') {
                    steps {
                        dir("service-b") {
                            sh 'sh test.sh'
                        }
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
