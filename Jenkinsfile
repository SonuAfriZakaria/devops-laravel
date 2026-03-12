pipeline {
    agent any

    environment {
        PROD_HOST = "172.21.19.121"
    }

    stages {

        stage('Build') {
            steps {
                script {
                    docker.image('composer:2.6').inside('--user root') {
                        sh 'composer install --no-interaction --prefer-dist'
                    }
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    docker.image('ubuntu').inside('--user root') {
                        sh 'echo Running test stage...'
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                sshagent(['ssh-prod']) {
                    sh '''
                    ssh -o StrictHostKeyChecking=no atmin@$PROD_HOST "
                        cd /home/atmin/devops-laravel &&
                        git pull origin main &&
                        php artisan migrate --force
                    "
                    '''
                }
            }
        }

    }
}
