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
        stage('Load git submodule') {
            steps {
                sh '''
                git submodule update --init --recursive
                '''
            }
        }
        stage('Set environment variables') {
            steps {
                script{
                    env.HOST = "m73-1.mandariini.uk"
                    env.DIR = "/srv/nfs/nginx-ville/"
                }
            }
        }
        stage('Build website') {
            steps {
                sh '''
                hugo
                '''
            }
        }
        stage('Publish website') {
            steps {
                sh '''
                rsync -e "ssh -o StrictHostKeyChecking=no -i $SSH_CREDS" -avz --delete public/ $SSH_CREDS_USR@$HOST:$DIR
                '''
            }
        }
    }
}