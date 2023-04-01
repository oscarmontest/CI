pipeline {
  agent {
    node {
      label 'aws'
    }

  }
  stages {
    stage('Init') {
      steps {
        dir(path: 'terraform') {
          sh 'terraform init'
        }

      }
    }

    stage('Plan') {
      steps {
        dir(path: 'terraform') {
          sh 'terraform plan'
        }

      }
    }

    stage('Apply') {
      when {
        branch 'main'
      }
      input {
        message 'Are you sure you want to apply?'
        id 'Deployment in proccess'
      }
      steps {
        dir(path: 'terraform') {
          sh 'terraform apply -auto-approve'
        }

      }
    }

    stage('Clean') {
      steps {
        dir(path: 'terraform') {
          sh 'rm -r .terraform/ && rm .terraform.* && rm terraform.*'
        }

      }
    }

  }
  environment {
    AWS_ACCESS_KEY_ID = credentials('aws_access_key_id')
    AWS_SECRET_ACCESS_KEY = credentials('aws_secret_access_key')
  }
  post {
    failure {
      echo 'There has been an error, check your configuration'
    }

    success {
      echo 'Deployment completed'
    }

  }
  options {
    disableConcurrentBuilds()
    ansiColor('xterm')
    timeout(time: 5, unit: 'MINUTES')
    timestamps()
  }
}