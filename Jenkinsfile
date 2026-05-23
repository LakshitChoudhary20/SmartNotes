pipeline {
agent any


stages {

    stage('Checkout') {
        steps {
            checkout scm
        }
    }

    stage('Deploy to AWS EC2') {

        steps {

            withCredentials([sshUserPrivateKey(credentialsId: 'aws-ec2-key', keyFileVariable: 'SSH_KEY')]) {

                sh '''
                ssh -i $SSH_KEY -o StrictHostKeyChecking=no ubuntu@65.2.129.28 "

                if [ ! -d 'smartnotes-project' ]; then git clone https://github.com/lakshitchoudhary20/smartnotes.git; fi &&

                cd smartnotes-project &&

                git pull origin main &&

                docker compose down &&

                docker compose up --build -d
                "
                '''
            }
        }
    }
}

}
