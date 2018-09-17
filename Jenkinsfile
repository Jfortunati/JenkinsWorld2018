pipeline {
  agent {
    node {
      label 'ESXI-AL-CI'
    }

  }
  stages {
    stage('Build') {
      steps {
        build 'deploy'
      }
    }
    stage('API Service Testing') {
      parallel {
        stage('API Service Testing') {
          steps {
            SoapUIPro(pathToTestrunner: 'test', pathToProjectFile: 'test', testSuite: 'test', testCase: 'test', projectPassword: 'test', environment: 'test')
          }
        }
        stage('') {
          steps {
            SoapUIPro(pathToTestrunner: 'C:\\tests_runner', pathToProjectFile: 'C:\\tests', testSuite: 'example', testCase: 'test', projectPassword: 'test', environment: 'test')
          }
        }
      }
    }
  }
}