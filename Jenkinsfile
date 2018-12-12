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

        stage('find upstream job') {
            steps {
                script {
                    def causes = currentBuild.rawBuild.getCauses()
                    for(cause in causes) {
                        if (cause.class.toString().contains("UpstreamCause")) {
                            println "This job was caused by job " + cause.upstreamProject
                        } else {
                            println "Root cause : " + cause.toString()
                        }
                    }
                }      
            }
        }

        stage('Build') {
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