pipeline {
    agent any
    stages {
        stage('initializing') {
            steps {
                bitbucketStatusNotify(buildName: 'ServiceA', buildState: 'INPROGRESS')
                bitbucketStatusNotify(buildName: 'ServiceB', buildState: 'INPROGRESS')
                bitbucketStatusNotify(buildName: 'ServiceC', buildState: 'INPROGRESS')
            }
        }
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
                echo "My BRANCH_NAME is: ${env.BRANCH_NAME}"
                echo "My CHANGE_TARGET is: ${env.CHANGE_TARGET}"
                echo "My BRANCHis: ${env.BRANCH}"
                echo "My GIT_BRANCH is: ${env.GIT_BRANCH}"
                echo "My GIT_PREVIOUS_SUCCESSFUL_COMMIT is: ${env.GIT_PREVIOUS_SUCCESSFUL_COMMIT}"
                sh 'echo "deploying"'
                // exit 1

                bitbucketStatusNotify(buildName: 'ServiceA', buildState: 'SUCCESSFUL')
                // bitbucketStatusNotify(buildName: 'ServiceB', buildState: 'SUCCESSFUL')
                bitbucketStatusNotify(buildName: 'ServiceC', buildState: 'SUCCESSFUL')
            }
        }
    }
}
