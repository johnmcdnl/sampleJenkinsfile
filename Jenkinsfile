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
            node{
                currentBuild.getUpstreamBuilds()
                    .collect { 
                        myObject -> echo myObject 
                    }
            }
            steps {
                // echo currentBuild.rawBuild.getCause(hudson.model.Cause$UpstreamCause)
                // echo currentBuild.getUpstreamBuilds()
                
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