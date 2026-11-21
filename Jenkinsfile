
pipeline {
    agent { label 'test' }

    options {
        skipDefaultCheckout(true)
        disableConcurrentBuilds()
    }

    stages {
        stage('Checkout Test Branch') {
            steps {
                dir('source') {
                    checkout scm
                }
            }
        }

        stage('Copy Files to Test') {
            steps {
                sh '''
                    mkdir -p /home/jenkins/deploy/test

                    rsync -av --delete \
                      --exclude='.git/' \
                      source/ /home/jenkins/deploy/test/

                    echo "Test deployment completed"
                    hostname
                    ls -la /home/jenkins/deploy/test/
                '''
            }
        }
    }

    post {
        success {
            echo 'Push-to-Test completed successfully!'
        }
        failure {
            echo 'Push-to-Test failed!'
        }
    }
}
