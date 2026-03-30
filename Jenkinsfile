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
                sh '/usr/local/bin/deploy-laravel.sh'
            }
        }
    }
}
