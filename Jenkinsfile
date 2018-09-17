pipeline {
  agent {
    node {
      customWorkspace 'C:\\Jenkins-Workspaces\\jenkins-world-2018'
      label 'ESXI-AL-CI'
    }

  }
  stages {
    stage('Build & Setup') {
      parallel {
        stage('Send to Staging') {
          steps {
            bat 'depoloy_script'
          }
        }
        stage('Start Virtual Services') {
          steps {
            bat 'alert_site.bat'
          }
        }
      }
    }
    stage('Unit Tests') {
      steps {
        waitUntil() {
          bat 'collaborator'
        }

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
    stage('Scalability Testing') {
      parallel {
        stage('Load UI') {
          steps {
            bat 'depoloy_script'
          }
        }
        stage('LoadComplete') {
          steps {
            bat 'alert_site.bat'
          }
        }
        stage('CrossBrowserTesting Automation') {
          steps {
            bat 'cbt.bat'
          }
        }
      }
    }
    stage('Deploy') {
      parallel {
        stage('Stop Virtual Services') {
          steps {
            bat 'depoloy_script'
          }
        }
        stage('Merge PR') {
          steps {
            bat 'depoloy_script'
          }
        }
        stage('Update Swagger Spec') {
          steps {
            bat 'swagger_spec.bat'
          }
        }
        stage('Update Jira') {
          steps {
            bat 'swagger_spec.bat'
          }
        }
        stage('Send to Prod') {
          steps {
            bat 'swagger_spec.bat'
          }
        }
      }
    }
    stage('Monitor') {
      steps {
        bat 'AlertSite Monitors'
      }
    }
  }
}