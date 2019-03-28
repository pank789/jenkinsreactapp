pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'npm install'
        echo 'NPM packages loaded'
      }
    }
    stage('Test') {
      steps {
        sh 'bash "./jenkins/scripts/test.sh"'
        input(message: 'Is test successful and ready to continue?', ok: 'Yes and continue to publish')
      }
    }
    stage('Deliver and stop ') {
      steps {
        sh 'bash "./jenkins/scripts/deliver.sh"'
        input(message: 'Have you tested react app', ok: 'yes successfully tested and continue to stop the server')
        sh 'bash "./jenkins/scripts/kill.sh"'
      }
    }
  }
  environment {
    CI = 'true'
    HOME = '.'
    PORT_NUMBER = '9090'
  }
}