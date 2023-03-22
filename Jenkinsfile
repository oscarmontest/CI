pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        echo 'Hello World'
      }
    }

    stage('Test') {
      steps {
        echo 'La vida son dos días'
      }
    }

    stage('Package') {
      steps {
        sh 'mvn compile'
      }
    }

  }
}