pipeline {
agent any

```
stages {

    stage('Checkout') {
        steps {
            checkout scm
        }
    }

    stage('Deploy to AWS EC2') {

        steps {

            sshagent(credentials: ['aws-ec2-key']) {

                sh '''
                ssh -o StrictHostKeyChecking=no ubuntu@65.2.129.28 "

                cd smartnotes-project &&

                git pull origin main &&

                cd backend &&

                mvn clean package &&

                cd .. &&

                docker compose down &&

                docker compose up --build -d
                "
                '''
            }
        }
    }
}
```

}
