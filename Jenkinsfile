pipeline {
    agent {
        node {
            label 'hugo'
            }
      }
    environment {
        SSH_CREDS = credentials('ssh-key')
    }
    triggers {
        pollSCM 'H/5 * * * *'
    }
    stages {
        stage('Build website') {
            steps {
                sh '''
                git submodule update --init --recursive
                hugo
                '''
            }
        }
        stage('Publish website') {
            steps {
                sh '''
                HOST=m73-1.mandariini.uk
                DIR=/srv/nfs/nginx-ville/
                rsync -e "ssh -o StrictHostKeyChecking=no -i $SSH_CREDS" -avz --delete public/ $SSH_CREDS_USR@${HOST}:${DIR}
                '''
            }
        }
    }
}