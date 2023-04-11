pipeline {
    agent {
        label('aws')
    }
    environment{
        AWS_ACCESS_KEY_ID = credentials('AWS_ACCESS_KEY_ID')
        AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
    }
    options { 
        disableConcurrentBuilds()
        ansiColor('xterm')
        timeout(time: 5, unit: 'MINUTES')
        timestamps()
    }
    stages {
        stage('Init') {
            steps {
                dir('terraform') {
                   sh '''cd www
                    terraform init'''
                }
            }
        }
        stage('Plan') {
            steps {
                dir('terraform') {
                   sh '''cd www
                   terraform plan'''
                }
            }
        }
        stage('Apply') {
            input {
                message "Confirm deployment"
                ok "Deploying..."
            }
            when  {
                branch 'dev'
            }
            steps {
                dir('terraform') {
                     sh '''cd www
                     terraform apply -auto-approve'''
              }
            }
        }
    }
    post {
        failure {
            echo "There has been an error, check your configuration"
        }
        success {
            echo "Deployment completed"
        }
    }
}
