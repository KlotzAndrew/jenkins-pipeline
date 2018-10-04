pipeline {
    agent any
    stages {
        stage('unit tests') {
            steps {
                checkout scm

                sh 'sh test.sh'
            }
        }
    }
}
