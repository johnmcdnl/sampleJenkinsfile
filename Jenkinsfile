pipeline {
  agent any
  stages {
    stage('Build Apps') {
      parallel {
        stage('TestSuite') {
          steps {
            echo 'Build TestSuite Started'
            sleep 4
            echo 'Build TestSuite Finished'
          }
        }
        stage('App1') {
          steps {
            echo 'Build App1 Started'
            sleep 3
            echo 'Build App1 Finished'
          }
        }
        stage('App2') {
          steps {
            echo 'Build App2 Started'
            sleep 5
            echo 'Build App2 Finished'
          }
        }
        stage('App3') {
          steps {
            echo 'Build App3 Started'
            sleep 1
            echo 'Build App3 Finished'
          }
        }
        stage('App4') {
          steps {
            echo 'Build App4 Started'
            sleep 4
            echo 'Build App4 Finished'
          }
        }
        stage('App5') {
          steps {
            echo 'Build App5 Started'
            sleep 8
            echo 'Build App5 Finished'
          }
        }
        stage('App6') {
          steps {
            echo 'Build App6 Started'
            sleep 3
            echo 'Build App6 Finished'
          }
        }
        stage('App7') {
          steps {
            echo 'Build App7 Started'
            sleep 8
            echo 'Build App7 Finished'
          }
        }
        stage('App8') {
          steps {
            echo 'Build App8 Started'
            sleep 4
            echo 'Build App8 Finished'
          }
        }
        stage('App9') {
          steps {
            echo 'Build App9 Started'
            sleep 7
            echo 'Build App9 Finished'
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
    quietPeriod(5)
    timestamps()
    // durabilityHint 'PERFORMANCE_OPTIMIZED'
    disableConcurrentBuilds()
    timeout(time: 1, unit: 'HOURS')
    parallelsAlwaysFailFast()
    skipStagesAfterUnstable()
    preserveStashes(buildCount: 5)
    buildDiscarder(logRotator(daysToKeepStr: '50', numToKeepStr: '50'))
  }
  triggers {
    upstream(threshold: hudson.model.Result.SUCCESS, upstreamProjects: 'fakeUpstreamProject/master')
    cron('H 07-19 * * *')
    pollSCM('* * * * *')
  }
}