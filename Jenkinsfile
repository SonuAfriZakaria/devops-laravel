pipeline {
    agent any

    stages {
        stage('Deploy to Production') {
            steps {
                sh '''
                ssh root@203.194.115.184 "/usr/local/bin/deploy-laravel.sh"
                '''
            }
        }
    }
}
