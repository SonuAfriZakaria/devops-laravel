node {

    environment {
        PROD_HOST = "host.docker.internal"
    }

    stage("Checkout") {
        checkout scm
    }

    stage("Build") {
        docker.image('composer:2.6').inside('-u root') {
            sh 'composer install --no-interaction --prefer-dist'
        }
    }

    stage("Test") {
        docker.image('ubuntu').inside('-u root') {
            sh 'echo "Running test stage..."'
        }
    }

    stage("Deploy") {
        docker.image('agung3wi/alpine-rsync:1.1').inside('-u root') {
            sshagent(credentials: ['ssh-prod']) {

                sh '''
                mkdir -p ~/.ssh

                ssh-keyscan -H $PROD_HOST >> ~/.ssh/known_hosts

                rsync -rav --delete ./ atmin@$PROD_HOST:/home/atmin/prod/ \
                --exclude=.env \
                --exclude=storage \
                --exclude=.git
                '''
            }
        }
    }

}
