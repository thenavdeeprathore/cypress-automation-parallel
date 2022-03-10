pipeline {

  agent any

//   agent {
//     docker {
//       image 'cypress/browsers:node16.5.0-chrome94-ff93'
//     }
//   }
  
  options {
      ansiColor('xterm')
  }
  
  stages {
    stage('checkout') {
      steps {
        checkout scm
      }
    }
    stage('build') {
      steps {
        sh 'npm i'
        sh 'npm run verify'
      }
    }
    stage('test') {
      steps {
        sh "npm run test:record"
      }
    }
  }

  post {
    // shutdown the server running in the background
    always {
      echo 'Tests are finished!'
    }
  }

}