node {
    checkout scm

    stage("Build") {
        docker.image('composer:2.6').inside('--entrypoint="" -u root') {
            sh 'composer install --no-interaction --prefer-dist'
        }
    }

    stage("Test") {
        docker.image('ubuntu').inside('--entrypoint="" -u root') {
            sh 'echo "Running test stage..."'
        }
    }

    stage("Deploy") {
        docker.image('agung3wi/alpine-rsync:1.1').inside('--entrypoint="" -u root') {
            sshagent(credentials: ['ssh-prod']) {
                sh '''
                mkdir -p ~/.ssh
                ssh-keyscan -H host.docker.internal >> ~/.ssh/known_hosts

                rsync -rav --delete ./ atmin@host.docker.internal:/home/atmin/prod/ \
                --exclude=.env \
                --exclude=storage \
                --exclude=.git
                '''
            }
        }
    }
}
