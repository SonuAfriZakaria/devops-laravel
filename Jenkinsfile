node {
    checkout scm

    // Build
    stage("Build"){
        docker.image('composer:2.6').inside('-u root') {
            sh 'composer install --no-interaction --prefer-dist'
        }
    }

    // Test
    stage("Test"){
        docker.image('ubuntu').inside('-u root') {
            sh 'echo "Ini adalah test pipeline Jenkins"'
        }
    }

    // Deploy
    stage("Deploy"){
    docker.image('agung3wi/alpine-rsync:1.1').inside('-u root') {
        sshagent(credentials: ['ssh-prod']) {
            sh '''
            mkdir -p ~/.ssh
            ssh-keyscan -H 172.21.19.121 >> ~/.ssh/known_hosts

            rsync -rav --delete ./ atmin@172.21.19.121:/home/atmin/prod/ \
            --exclude=.env \
            --exclude=storage \
            --exclude=.git
            '''
        }
    }
}
}
