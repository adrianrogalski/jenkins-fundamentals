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
          chmod +x test.sh
          ./test.sh
        '''
      }
    }
    stage('Test') {
      steps {
        echo "Testing. I can see release ${RELEASE}"
      }
    }
    stage('Deploy') {
      input {
        message 'Deploy?'
        ok 'Do it!'
        parameters {
          string(name: 'TARGET_ENVIRONMENT', defaultValue: 'PROD', description: 'Target deployment environment')
        }
      }
      parallel {
        stage('linux-arm64') {
          steps {
            echo "Deploying release ${RELEASE} to environment ${TARGET_ENVIRONMENT}"
          }
        }
        stage('linux-amd64') {
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
      always {
        echo "Pipeline executed"
      }
    }
}