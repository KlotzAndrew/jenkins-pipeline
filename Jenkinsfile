pipeline {
    agent any
    stages {
        stage('unit tests') {
            steps {
                sh 'sh test.sh'
            }
            steps {
                sh 'sh test.sh'
            }
        }
        stage('integration tests') {
            steps {
                sh 'sh test.sh'
            }
        }
    }
}
