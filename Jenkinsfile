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
            bat(returnStdout: true, script: '.\\staging.bat')
          }
        }
        stage('Start Virtual Services') {
          steps {
            bat(returnStdout: true, script: '.\\start-virt-serv.bat')
          }
        }
      }
    }
    stage('Unit Tests') {
      steps {
        waitUntil() {
          bat(returnStdout: true, script: '.\\unit-tests.bat')
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
            bat(returnStdout: true, script: '.\\test-complete.bat')
          }
        }
        stage('Legacy Selenium') {
          steps {
            bat(returnStdout: true, script: '.\\selenium.bat')
          }
        }
      }
    }
    stage('BDD Scenarios') {
      steps {
        bat(returnStdout: true, script: '.\\bdd.bat')
      }
    }
    stage('Peer Review') {
      steps {
        waitUntil() {
          bat(returnStdout: true, script: '.\\collaborator.bat')
        }

      }
    }
    stage('Scalability Testing') {
      parallel {
        stage('Load UI') {
          steps {
            bat(returnStdout: true, script: '.\\loadui.bat')
          }
        }
        stage('LoadComplete') {
          steps {
            bat(returnStdout: true, script: '.\\loadcomplete.bat')
          }
        }
        stage('CrossBrowserTesting Automation') {
          steps {
            bat(returnStdout: true, script: '.\\cbt.bat')
          }
        }
      }
    }
    stage('Deploy') {
      parallel {
        stage('Stop Virtual Services') {
          steps {
            bat(returnStdout: true, script: '.\\stop-virt-serv.bat')
          }
        }
        stage('Merge PR') {
          steps {
            bat(returnStdout: true, script: '.\\merge.bat')
          }
        }
        stage('Update Swagger Spec') {
          steps {
            bat(returnStdout: true, script: '.\\swagger.bat')
          }
        }
        stage('Update Jira') {
          steps {
            bat(returnStdout: true, script: '.\\jira.bat')
          }
        }
        stage('Send to Prod') {
          steps {
            bat(returnStdout: true, script: '.\\prod.bat')
          }
        }
      }
    }
    stage('Monitor') {
      steps {
        bat(returnStdout: true, script: '.\\alertsite.bat')
      }
    }
  }
}