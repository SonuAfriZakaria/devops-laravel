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

    // Deploy
    stage("Deploy"){
        docker.image('agung3wi/alpine-rsync:1.1').inside('-u root') {
            sshagent (credentials: ['ssh-prod']) {
                sh 'mkdir -p ~/.ssh'
                sh 'ssh-keyscan -H "$PROD_HOST" > ~/.ssh/known_hosts'
                sh "rsync -rav --delete ./ ubuntu@$PROD_HOST:/home/ubuntu/prod/ --exclude=.env --exclude=storage --exclude=.git"
            }
        }
    }
}
