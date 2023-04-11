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
                    sh 'terraform init'
                }
            }
        }
        stage('Plan') {
            steps {
                dir('terraform') {
                    sh 'terraform plan'
                }
            }
        }
        stage('Apply') {
            input {
                message "Are you sure you want to apply?"
                ok "Deployment in proccess"
            }
            when  {
                branch 'main'
            }
            steps {
                dir('terraform') {
                    sh 'terraform apply -auto-approve'
                }
            }
        }

        stage('Clean') {
            steps {
                dir('terraform') {
                    sh 'rm -r .terraform/ && rm .terraform.* && rm terraform.*'
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
