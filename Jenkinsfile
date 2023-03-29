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
        echo 'La vida son dos días'
        sh 'mvn test'
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