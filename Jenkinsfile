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
            # Tambahkan safe directory untuk user www-data
            sudo -u www-data git config --global --add safe.directory /var/www/laravel-devops
            
            # Jalankan git pull sebagai www-data
            cd /var/www/laravel-devops
            sudo -u www-data git pull origin main
            
            # Lanjutkan dengan perintah lainnya
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
