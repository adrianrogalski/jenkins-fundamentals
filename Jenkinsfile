pipeline {
  agent any
  stages {
    stage('stage1') {
      steps {
        sh '''echo "This build $BUILD_NUMBER of demo $DEMO"
'''
      }
    }

  }
  environment {
    DEMO = '1'
  }
}