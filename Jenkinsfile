pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/user/repo.git'
            }
        }

        stage('Build') {
            steps {
                sh 'echo "Build berjalan..."'
            }
        }

        stage('Test') {
            steps {
                sh 'echo "Testing berjalan..."'
            }
        }

        stage('Deploy') {
            steps {
                sh 'echo "Deploy berjalan..."'
            }
        }
    }
}
