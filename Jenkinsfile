pipeline {
    agent any
    stages {
        stage('unit tests') {
            failFast true
            parallel {
                stage('service a') {
                    steps {
                        sh 'sh test.sh'
                    }
                }
                stage('service b') {
                    steps {
                        sh 'sh test.sh'
                    }
                }
            }
        }
        stage('integration tests') {
            steps {
                sh 'sh test.sh'
            }
        }
    }
}
