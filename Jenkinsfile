
pipeline {
    agent { label 'prod' }

    options {
        skipDefaultCheckout(true)
        disableConcurrentBuilds()
    }

    stages {
        stage('Checkout Master Branch') {
            steps {
                dir('source') {
                    checkout scm
                }
            }
        }

        stage('Copy Files to Production') {
            steps {
                sh '''
                    mkdir -p /home/jenkins/deploy/prod

                    rsync -av --delete \
                      --exclude='.git/' \
                      source/ /home/jenkins/deploy/prod/

                    echo "Production deployment completed"
                    hostname
                    ls -la /home/jenkins/deploy/prod/
                '''
            }
        }
    }

    post {
        success {
            echo 'Push-to-Prod completed successfully!'
        }
        failure {
            echo 'Push-to-Prod failed!'
        }
    }
}
