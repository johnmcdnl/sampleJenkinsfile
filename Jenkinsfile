pipeline {

    agent any

    stages {
        stage() {
            parallel {
                stage('Build Test Suite') {
                    steps {
                        echo 'Build Test Suite'
                    }
                }
                stage('Build Apps') {
                    steps {
                        echo 'Here will build the correct version of each project under test'
                    }
                }
            }
        }

        stage('Dockerise Apps') {
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
                echo "TAS_USERNAME ${TAS_USERNAME}"
                echo "TAS_PASSWORD ${TAS_PASSWORD}"
                echo 'Test Complete'
            }
        }

        stage('Report') {
            steps {
                echo 'Report the results'
            }
        }
    }

    options {
        disableConcurrentBuilds()
        buildDiscarder(
            logRotator(
                daysToKeepStr: '50', 
                numToKeepStr: '50'
            )
        )
        timeout(time: 1, unit: 'HOURS')
        parallelsAlwaysFailFast()
    }

    environment {
        USER_CREDENTIALS = credentials('tas_john')
        BROWSER = "firefox"
        BROWSER_HEADLESS_MODE = "true"
        USERNAME = "${USER_CREDENTIALS_USR}"
        PASSWORD = "${USER_CREDENTIALS_PSW}"
    }

    triggers {
        upstream(
            threshold: hudson.model.Result.SUCCESS, 
            upstreamProjects: 'fakeUpstreamProject/master'
        )
        cron('H 07-19 * * *')
        pollSCM('* * * * *')
    }

    post {
        always {
            echo "do this always"
            // node {
            //     sh 'printenv'
            // }
        }

        // regression {
        //     emailext (
        //         body: 'regression', 
        //         subject: 'SampleJenkinsfile regression', 
        //         to: 'john.mcdonnell@email.com'
        //     )
        // }
        
        // unsuccessful {
        //     emailext (
        //         body: 'unsuccessful', 
        //         subject: 'SampleJenkinsfile unsuccessful', 
        //         to: 'john.mcdonnell@email.com'
        //     )
        // }

        // fixed {
        //     emailext (
        //         body: 'fixed', 
        //         subject: 'SampleJenkinsfile fixed', 
        //         to: 'john.mcdonnell@email.com'
        //     )
        // }

        cleanup {
            echo "do this cleanup"
        }

    }

}