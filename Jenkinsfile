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
        bat(script: '.\\collaborator.bat', returnStdout: true)
      }
    }
	
    stage('API') {
      parallel {
        stage('SoapUI Tests') {
          steps {
            bat(script: '.\\collaborator.bat', returnStdout: true)
          }
        }
        stage('SecureV Tests') {
          steps {
            bat(script: '.\\collaborator.bat', returnStdout: true)
          }
        }
      }
    }
    stage('End to End') {
      parallel {
        stage('TestComplete Automation') {
          steps {
            bat(script: '.\\collaborator.bat', returnStdout: true)
          }
        }
        stage('CrossBrowserTesting & Selenium') {
          steps {
            bat(script: '.\\collaborator.bat', returnStdout: true)
          }
        }
        stage('Update Hiptest BDD Scenarios') {
          steps {
            bat(script: '.\\collaborator.bat', returnStdout: true)
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
            bat(script: '.\\collaborator.bat', returnStdout: true)
          }
        }
        stage('LoadComplete') {
          steps {
            bat(script: '.\\collaborator.bat', returnStdout: true)
          }
        }
        stage('CrossBrowserTesting Automation') {
          steps {
            bat(script: '.\\collaborator.bat', returnStdout: true)
          }
        }
      }
    }
    stage('Deploy') {
      parallel {
        stage('Stop Virtual Services') {
          steps {
            bat(script: '.\\collaborator.bat', returnStdout: true)
          }
        }
        stage('Merge PR') {
          steps {
            bat(script: '.\\collaborator.bat', returnStdout: true)
          }
        }
        stage('Update Swagger Spec') {
          steps {
            bat(script: '.\\collaborator.bat', returnStdout: true)
          }
        }
        stage('Update Jira') {
          steps {
            bat(script: '.\\collaborator.bat', returnStdout: true)
          }
        }
        stage('Send to Prod') {
          steps {
            bat(script: '.\\collaborator.bat', returnStdout: true)
          }
        }
		stage('Announce Successful Deployment to Slack') {
          steps {
            bat(script: '.\\collaborator.bat', returnStdout: true)
          }
        }
      }
    }
    stage('Monitor') {
      steps {
        bat(script: '.\\collaborator.bat', returnStdout: true)
        echo 'test'
      }
    }
  }
}