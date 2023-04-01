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
          sh '''cd /home/terraform/www
terraform init'''
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