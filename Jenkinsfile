@NonCPS
def getBranchNames(project){
    echo "start getBranchNames"
    project.getItems().each { job ->
        echo job.getProperty(org.jenkinsci.plugins.workflow.multibranch.BranchJobProperty.class).getBranch().getName()
    }
    echo "end getBranchNames"
}

pipeline {

    agent any

    stages {
        stage('find upstream job') {
            steps {
                script {
                def upstreamBuilds = currentBuild.getUpstreamBuilds()
                    for(upstreamBuild in upstreamBuilds) {
                        println "1) upstreamBuild.getFullProjectName().minus(upstreamBuild.getProjectName() : " + upstreamBuild.getFullProjectName().minus(upstreamBuild.getProjectName())
                        println "2) upstreamBuild.getFullProjectName() : " + upstreamBuild.getFullProjectName()
                        println "3) upstreamBuild.getProjectName() : " + upstreamBuild.getProjectName()

                        getBranchNames(
                            jenkins.model.Jenkins.instance.getItem(
                                upstreamBuild.getFullProjectName().minus("/" + upstreamBuild.getProjectName())
                            )
                        )
                    }
                }
            }
        }

        stage('Build') {
            parallel {
                stage('Build parallel Stage 1') {
                    steps {
                        echo 'Build'
                    }
                }
                stage('Build parallel Stage 2') {
                    steps {
                        echo 'Another Branch!'
                    }
                }
            }
        }

        stage('Test') {
            steps {
                echo 'Test'
                echo "${USER_CREDENTIALS_USR}"
                echo "${USER_CREDENTIALS_PSW}"
                
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploy'
                sh 'printenv'
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
        timeout(
            time: 1, 
            unit: 'HOURS'
        )
        parallelsAlwaysFailFast()
    }

    parameters {
        credentials (
            credentialType: 'com.cloudbees.plugins.credentials.impl.UsernamePasswordCredentialsImpl', 
            defaultValue: 'tas_john', 
            description: 'tas_john', 
            name: 'tas_john', 
            required: true
        )
    }

    environment {
        USER_CREDENTIALS = credentials('tas_john')
    }

    triggers {
        upstream(
            threshold: hudson.model.Result.SUCCESS, 
            upstreamProjects: 'fakeUpstreamProject/master')
        cron('H 07-19 * * *')
        pollSCM('* * * * *')
    }

    post {
        always {
            
        }

        regression {
            emailext (body: 'regression', subject: 'SampleJenkinsfile regression', to: 'john.mcdonnell@aotal.com')
        }
        
        unsuccessful {
            emailext (body: 'unsuccessful', subject: 'SampleJenkinsfile unsuccessful', to: 'john.mcdonnell@aotal.com')
        }

        fixed {
            emailext (body: 'fixed', subject: 'SampleJenkinsfile fixed', to: 'john.mcdonnell@aotal.com')
        }

        cleanup {
            
        }

    }

}