node {
    checkout scm

    // Build
    stage("Build"){
        docker.image('composer:2.6').inside('-u root') {
            sh 'composer install --no-interaction --prefer-dist'
        }
    }

    // Testing
    stage("Test"){
        docker.image('ubuntu').inside('-u root') {
            sh 'echo "Ini adalah test"'
        }
    }
}
