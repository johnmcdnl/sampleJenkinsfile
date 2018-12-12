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
        pollSCM('* * * * *') 
    }

    stages {
        stage('Build') {

            steps {
                // echo currentBuild.rawBuild.getCause(hudson.model.Cause$UpstreamCause)
                // echo currentBuild.getUpstreamBuilds()
                currentBuild.getUpstreamBuilds().collect { it -> echo it }
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