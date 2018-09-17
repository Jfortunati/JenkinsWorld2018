pipeline {
  agent {
    node {
      customWorkspace 'C:\\Jenkins-Workspaces\\jenkins-world-2018'
      label 'ESXI-AL-CI'
    }

  }
  stages {
    stage('Virtual Services') {
      steps {
        build 'deploy'
      }
    }
    stage('Regression') {
      parallel {
        stage('SoapUI Tests') {
          steps {
            SoapUIPro(pathToTestrunner: 'test', pathToProjectFile: 'test', testSuite: 'test', testCase: 'test', projectPassword: 'test', environment: 'test')
          }
        }
        stage('TestComplete Tests') {
          steps {
            bat 'test_complete.bat'
            bat 'selenium_scripts.bat'
          }
        }
        stage('Legacy Selenium') {
          steps {
            bat 'myscripts.bat'
          }
        }
      }
    }
    stage('BDD Scenarios') {
      steps {
        bat 'testcomplete'
      }
    }
    stage('Peer Review') {
      steps {
        waitUntil() {
          bat 'collaborator'
        }

      }
    }
    stage('Deploy') {
      parallel {
        stage('Deploy') {
          steps {
            bat 'depoloy_script'
          }
        }
        stage('AlertSite Monitors') {
          steps {
            bat 'alert_site.bat'
          }
        }
        stage('Update Swagger Spec') {
          steps {
            bat 'swagger_spec.bat'
          }
        }
      }
    }
  }
}
