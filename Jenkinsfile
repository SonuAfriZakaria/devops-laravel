pipeline {
    agent any

    stages {
        stage('Deploy to VPS') {
            steps {
                sh '''
                rm -rf /var/www/laravel-devops/*
                cp -r ./* /var/www/laravel-devops/
                '''
            }
        }
    }
}
