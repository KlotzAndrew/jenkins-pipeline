pipeline {
    agent any
    stages {
        stage('unit tests') {
            steps {
                sh 'sh test.sh'
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
