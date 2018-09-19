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
        echo 'buliding application...'
		echo 'deploying to environment STAGING...'
		echo 'deployment complete'
      }
    }
    stage('Start ServiceV Pro') {
      steps {
        echo 'starting virtual services...'
      }
    }
    stage('Unit Tests') {
      steps {
        echo 'running unit tests...'
		echo 'running static analysis...'
		echo 'all tests passed'
      }
    }
	
    stage('API') {
      parallel {
        stage('SoapUI Pro Tests') {
          steps {
            echo 'running SoapUI Pro tests...'
			echo 'SoapUI Pro testing complete: 4/4 pass, 0/4 fail'
          }
        }
        stage('Secure Pro Tests') {
          steps {
            echo 'running Secure Pro tests...'
			echo 'Secure Pro testing complete: 2/2 pass, 0/2 fail'
          }
        }
      }
    }
    stage('End to End') {
      parallel {
        stage('TestComplete Automation') {
          steps {
            echo 'running TestComplete tests...'
			echo 'TestComplete testing complete: 2/2 pass, 0/2 fail'
          }
        }
        stage('CrossBrowserTesting & Selenium') {
          steps {
            echo 'running selenium scripts...'
			echo 'running CBT visual comparison...'
			echo 'all selenium scripts passed'
			echo 'CBT visual comparison within bounds, 2 differences found'
          }
        }
        stage('Update Hiptest BDD Scenarios') {
          steps {
            echo 'Hiptest scenarios updated'
          }
        }
      }
    }
    stage('Peer Review') {
      steps {
        echo 'Collaborator review completed'
      }
    }
    stage('Scalability Testing') {
      parallel {
        stage('Load UI Pro') {
          steps {
            echo 'starting LoadUI Pro testing...'
			echo 'LoadUI testing complete: 2/2 passed, 0/2 failed'
          }
        }
        stage('LoadComplete') {
          steps {
            echo 'starting LoadComplete testing...'
			echo 'LoadComplete testing complete: 2/2 passed, 0/2 failed'
          }
        }
       }
    }
    stage('Deploy') {
      parallel {
        stage('Stop Virtual Services') {
          steps {
            echo 'stopping virtual services...'
          }
        }
        stage('Merge PR') {
          steps {
            echo 'code merged from branch SPRINT-15 to branch PROD'
          }
        }
        stage('Update Swagger Spec') {
          steps {
            echo 'SwaggerHub updated, spec PUBLISHED as V1.2.1'
          }
        }
        stage('Update Jira') {
          steps {
            echo 'updating Jira tasks with tag SPRINT-15 to DONE'
          }
        }
        stage('Send to Prod') {
          steps {
            echo 'buliding application...'
			echo 'deploying to environment PROD...'
			echo 'deployment complete'
          }
        }
		stage('Slack Message!') {
          steps {
            echo 'sending message to channel DEPLOYMENTS as SUCCESSFUL'
          }
        }
      }
    }
    stage('Monitor') {
      steps {
        echo 'adding SoapUI Pro tests as monitors to Alertsite'
      }
    }
  }
}
