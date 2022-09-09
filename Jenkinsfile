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
          echo "Using multiline shell step"
          ./test.sh
        '''
      }
    }
    stage('Test') {
      steps {
        echo "Testing. I can see release ${RELEASE}..."
      }
    }
  }
}