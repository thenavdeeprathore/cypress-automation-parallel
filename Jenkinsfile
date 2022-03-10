pipeline {
  agent {
    docker {
      image 'cypress/base:10'
    }
  }

  stages {
    stage('checkout') {
      steps {
        checkout scm
      }
    }
    stage('build') {
      steps {
        sh 'npm ci'
      }
    }
    stage('test') {
      steps {
        sh "npm run test:record"
      }
    }
  }
}