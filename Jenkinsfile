pipeline{
  agent {
    label 'master'
  }
stages{
    stage('Build') {
        steps{
            sh 'npm install'
            sh 'ls'
        }
    }
    stage('Deploy') {
    environment {
        EC2_HOST = '13.232.21.133'
        EC2_USER = 'ubuntu'
        }
    steps {
            sh '''
            scp -o "StrictHostKeyChecking=no" -r ./ ${EC2_USER}@${EC2_HOST}:/home/${EC2_USER}/nodeapp
            ssh -o "StrictHostKeyChecking=no" -i ${SSH_KEY} ${EC2_USER}@${EC2_HOST} "cd /home/${EC2_USER}/nodeapp && npm install && pm2 start app.js --name "my node app""
            '''
            }
        }
      }

    }
}
