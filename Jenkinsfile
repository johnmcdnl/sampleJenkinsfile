pipeline {
  agent any
  stages {
    stage('Build Apps') {
      parallel {
        stage('TestSuite') {
          steps {
            echo 'Build TestSuite'
            sleep 4
          }
        }
        stage('App1') {
          steps {
            echo 'Build App1'
            sleep 3
          }
        }
        stage('App2') {
          steps {
            echo 'Build App2'
            sleep 5
          }
        }
        stage('App3') {
          steps {
            echo 'Build App3'
            sleep 1
          }
        }
        stage('App4') {
          steps {
            echo 'Build App4'
            sleep 4
          }
        }
        stage('App5') {
          steps {
            echo 'Build App5'
            sleep 8
          }
        }
        stage('App6') {
          steps {
            echo 'Build App6'
            sleep 3
          }
        }
        stage('App7') {
          steps {
            echo 'Build App7'
            sleep 8
          }
        }
        stage('App8') {
          steps {
            echo 'Build App8'
            sleep 4
          }
        }
        stage('App9') {
          steps {
            echo 'Build App9'
            sleep 7
          }
        }
      }
    }
    stage('Dockerise') {
      steps {
        echo 'Start docker-compose here'
      }
    }
    stage('Test') {
      options {
        retry(3)
      }
      steps {
        echo 'Test'
        echo "USER_CREDENTIALS_USR ${USER_CREDENTIALS_USR}"
        echo "USER_CREDENTIALS_PSW ${USER_CREDENTIALS_PSW}"
        echo "USERNAME ${USERNAME}"
        echo "PASSWORD ${PASSWORD}"
        echo 'Test Complete'
      }
    }
    stage('Report') {
      steps {
        echo 'Report the results'
      }
    }
  }
  environment {
    USER_CREDENTIALS = credentials('tas_john')
    BROWSER = 'firefox'
    BROWSER_HEADLESS_MODE = 'true'
    USERNAME = "${USER_CREDENTIALS_USR}"
    PASSWORD = "${USER_CREDENTIALS_PSW}"
  }
  post {
    always {
      echo 'do this always'

    }

    cleanup {
      echo 'do this cleanup'
      echo 'docker-compose down'

    }

  }
  options {
    disableConcurrentBuilds()
    buildDiscarder(logRotator(daysToKeepStr: '50', numToKeepStr: '50'))
    timeout(time: 1, unit: 'HOURS')
    parallelsAlwaysFailFast()
  }
  triggers {
    upstream(threshold: hudson.model.Result.SUCCESS, upstreamProjects: 'fakeUpstreamProject/master')
    cron('H 07-19 * * *')
    pollSCM('* * * * *')
  }
}