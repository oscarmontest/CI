pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        echo 'Building Artifacts...'
        sh 'mvn compile -f /var/lib/jenkins/keys/pom.xml'
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
