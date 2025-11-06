pipeline {
    agent {
        node {
            label 'hugo'
            }
      }
    environment {
        SSH_CREDS = credentials('ssh-key')
    }
    stages {
        stage('Build') {
            steps {
                echo "Building website"
                sh '''
                git submodule update --init --recursive
                hugo
                '''
            }
        }
        stage('Publish') {
            steps {
                echo 'Publishing website'
                sh '''
                HOST=m73-1.mandariini.uk
                DIR=/srv/nfs/nginx-ville/
                rsync -e "ssh -o StrictHostKeyChecking=no -i $SSH_CREDS" -avz --delete public/ $SSH_CREDS_USR@${HOST}:${DIR}
                '''
            }
        }
    }
}