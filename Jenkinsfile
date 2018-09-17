pipeline {
  agent {
    node {
      customWorkspace 'C:\\Jenkins-Workspaces\\jenkins-world-2018'
      label 'ESXI-AL-CI'
    }

  }
  stages {
    stage('Deploy to Staging') {
      steps {
        bat(script: '.\\collaborator.bat', returnStdout: true)
      }
    }
    stage('Start Virtual Services') {
      steps {
        bat(script: '.\\collaborator.bat', returnStdout: true)
      }
    }
    stage('Unit Tests') {
      steps {
        bat(script: '.\\unit-tests.bat', returnStdout: true)
      }
    }
	
    stage('API') {
      parallel {
        stage('SoapUI Tests') {
          steps {
            bat(returnStdout: true, script: '.\\test-complete.bat')
          }
        }
        stage('SecureV Tests') {
          steps {
            bat(returnStdout: true, script: '.\\test-complete.bat')
          }
        }
      }
    }
    stage('End to End') {
      parallel {
        stage('TestComplete Automation') {
          steps {
            bat(returnStdout: true, script: '.\\test-complete.bat')
          }
        }
        stage('CrossBrowserTesting & Selenium') {
          steps {
            bat(returnStdout: true, script: '.\\test-complete.bat')
          }
        }
        stage('Update Hiptest BDD Scenarios') {
          steps {
            bat(returnStdout: true, script: '.\\selenium.bat')
          }
        }
      }
    }
    stage('Peer Review') {
      steps {
        bat(script: '.\\collaborator.bat', returnStdout: true)
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
		stage('Announce Successful Deployment to Slack') {
          steps {
            bat(returnStdout: true, script: '.\\prod.bat')
          }
        }
      }
    }
    stage('Monitor') {
      steps {
        bat(returnStdout: true, script: '.\\alertsite.bat')
        echo 'test'
      }
    }
  }
}