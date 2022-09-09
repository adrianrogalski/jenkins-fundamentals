pipeline {
  agent any
  environment {
    RELEASE='20.04'
  }
  stages {
    stage('Build') {
      agent any
      environment {
        LOG_LEVEL='INFO'
      }
      steps {
        echo "Building release ${RELEASE} with log level ${LOG_LEVEL}...."
        sh '''
          echo "Using multili0ne shell step"
          chmod +x test.sh
          ./test.sh
        '''
      }
    }
    stage('Test') {
      steps {
        echo "Testing. I can see release ${RELEASE}"
        writeFile file: 'test-results.txt', text: 'passed'
      }
    }
    stage('Deploy') {
      parallel {
        stage('linux-arm64') {
          steps {
            echo "Deploying release ${RELEASE} to environment ${TARGET_ENVIRONMENT}"
          }
        }
        stage('windows-amd64') {
          steps {
            echo "Deploying release ${RELEASE} to environment ${TARGET_ENVIRONMENT}"
          }
        }
      }
    }
  }
   post {
      success {
        archiveArtifacts 'test-results.txt'
        echo "File archived"
      }
    }
}