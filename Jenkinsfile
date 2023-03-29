pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        echo 'Check /var/log Space'
        sh 'df -h /var/log'
      }
    }

    stage('Test') {
      steps {
        echo 'Pack the folders'
        sh 'tar zcf /home/jenkins/logs.tar /var/log'
      }
    }

    stage('Exex') {
      steps {
        echo 'Executing...'
        sh 'mvn exec:java'
      }
    }

    stage('OK') {
      steps {
        sleep 10
      }
    }

  }
}