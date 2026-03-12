pipeline {
    agent any

    environment {
        PROD_HOST = "host.docker.internal"  // ganti sesuai server prod-mu
        PROJECT_PATH = "/home/atmin/devops-laravel"
        LARAVEL_PORT = "8000"
    }

    stages {

        stage('Build') {
            steps {
                script {
                    // Install dependencies dengan Composer di Docker
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
            sh """
            ssh -o StrictHostKeyChecking=no atmin@$PROD_HOST '
                cd $PROJECT_PATH
                git pull origin main
                
                sudo chown -R atmin:www-data storage bootstrap/cache
                sudo chmod -R 775 storage bootstrap/cache

                php artisan migrate --force
                php artisan config:cache
                php artisan route:cache

                # Build & restart Docker containers
                docker-compose down
                docker-compose up -d --build

                echo "Laravel deployed and running at http://$PROD_HOST"
            '
            """
                }
            }
        }

    }
}
