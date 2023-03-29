pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        echo 'Building Artifacts...'
        sh '''def output = sh(returnStdout: true, returnStdoutTrim: true, script: \'df -h /tmp | awk \'{print $5}\' | grep -v Use |sed \'s/.$//\'\')
                    if (output > 70) {
                        echo "Warning Space"
                    } else {
                        echo "All is successfully"
                    }'''
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