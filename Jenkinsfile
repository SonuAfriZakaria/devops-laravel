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
                sshagent(['atmin']) {
                    sh """
                    mkdir -p /root/.ssh
                    ssh-keyscan -H ${PROD_HOST} >> /root/.ssh/known_hosts

                    rsync -avz --delete ./ atmin@${PROD_HOST}:/home/atmin/devops-laravel/

                    ssh atmin@${PROD_HOST} '
                        cd /home/atmin/devops-laravel &&
                        docker compose down &&
                        docker compose up -d --build
                    '
                    """
                }
            }
        }
    }
}
