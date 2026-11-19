
pipeline {
    agent any

    options {
        skipDefaultCheckout(true)
    }

    stages {
        stage('Checkout Git Repository') {
            steps {
                dir('source') {
                    checkout scm
                }
            }
        }

        stage('Verify Downloaded Files') {
            steps {
                sh '''
                    echo "Assignment 1 - Git Checkout"
                    pwd
                    ls -la source/
                    git -C source branch --show-current
                    git -C source log -1 --oneline
                '''
            }
        }
    }

    post {
        success {
            echo 'Assignment 1 completed successfully!'
        }
        failure {
            echo 'Assignment 1 failed!'
        }
    }
}
