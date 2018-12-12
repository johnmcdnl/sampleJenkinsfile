pipeline {

    agent any

    options{
        disableConcurrentBuilds()
        buildDiscarder(logRotator(daysToKeepStr: '50',numToKeepStr: '50'))
        timeout(time: 1, unit: 'HOURS')
        parallelsAlwaysFailFast()
    }

    triggers {
        upstream (threshold: hudson.model.Result.SUCCESS,upstreamProjects: 'project-name-1')
        cron('H 07-19 * * *')
    }

    stages {
        stage('Build') {

            // def upstream = currentBuild.rawBuild.getCause(hudson.model.Cause$UpstreamCause)
            // echo upstream?.shortDescription
            // echo "***"
            // echo upstream
            // echo "***"

            steps {
                echo 'Build'
            }
        }

        stage('Test') {

            steps {
                echo 'Test'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploy'
            }
        }
        
    }

}