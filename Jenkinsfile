pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'echo "Build stage - source code checked out"'
            }
        }
        stage('Test') {
            steps {
                sh 'echo "Test stage - running tests"'
            }
        }
        stage('Deploy') {
            steps {
                sh '''
                cd /var/www/laravel-devops
                git pull origin main
                composer install --no-dev --optimize-autoloader --no-interaction
                php artisan migrate --force
                php artisan config:clear
                php artisan cache:clear
                php artisan view:clear
                chown -R www-data:www-data storage bootstrap/cache
                chmod -R 775 storage bootstrap/cache
                '''
            }
        }
    }
}
