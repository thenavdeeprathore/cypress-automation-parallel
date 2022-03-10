@Library('pipeline') _

pipeline {
  agent {
    docker {
      image 'cypress/browsers:node16.5.0-chrome94-ff93'
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
        sh 'npm run verify'
      }
    }
    stage('test') {
      steps {
        sh "npm run test:record"
      }
    }
  }
}