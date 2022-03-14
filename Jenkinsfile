pipeline {

  agent {
    docker {
      image 'cypress/browsers:node16.5.0-chrome94-ff93'
    }
  }
  
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
    stage('cypress parallel tests') {
      parallel {
        // start several test jobs in parallel, and they all
        // will use Cypress Dashboard to load balance any found spec files
        stage('tester A') {
          steps {
            echo "Running build ${env.BUILD_ID}"
            sh "npm run test:record"
          }
        }

        // second tester runs the same command
        stage('tester B') {
          steps {
            echo "Running build ${env.BUILD_ID}"
            sh "npm run test:record"
          }
        }
      }
    }
    
    // stage('build and test') {
    //   // agent {
    //   //   docker {
    //   //     image 'cypress/browsers:node16.5.0-chrome94-ff93'
    //   //   }
    //   // }
    //   steps {
    //     checkout scm
    //     sh 'npm i'
    //     sh 'npm run verify'
    //     sh "npm run test:record"
    //   }
    // }
  }

  post {
    // shutdown the server running in the background
    always {
      echo 'Tests are finished!'
    }
  }

}