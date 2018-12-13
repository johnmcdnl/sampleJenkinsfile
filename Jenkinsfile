pipeline {

    agent any

    stages {
        stage('Build Apps') {
            parallel {
                stage('TestSuite') {steps {
                    echo 'Build TestSuite'
                    sh "sleep 5"
                }}
                stage('App1') {steps {
                    echo 'Build App1'
                    sh "sleep 5"
                }}
                stage('App2') {steps {
                    echo 'Build App2'
                    sh "sleep 5"
                }}
               stage('App3') {steps {
                    echo 'Build App3'
                    sh "sleep 5"
                }}
               stage('App4') {steps {
                    echo 'Build App4'
                    sh "sleep 5"
                }}
                stage('App5') {steps {
                    echo 'Build App5'
                    sh "sleep 5"
                }}
                stage('App6') {steps {
                    echo 'Build App6'
                    sh "sleep 5"
                }}
                stage('App7') {steps {
                    echo 'Build App7'
                    sh "sleep 5"
                }}
                stage('App8') {steps {
                    echo 'Build App8'
                    sh "sleep 5"
                }}
                stage('App9') {steps {
                    echo 'Build App9'
                    sh "sleep 5"
                }}
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
            echo "docker-compose down"
        }

    }

}