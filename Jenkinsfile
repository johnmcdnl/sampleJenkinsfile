@NonCPS
def getBranchNames(project){
    project.getItems().each { job ->
        echo job.getProperty(org.jenkinsci.plugins.workflow.multibranch.BranchJobProperty.class).getBranch().getName()
    }
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


        getBranchNames(jenkins.model.Jenkins.instance.getItem(
            env.JOB_NAME.minus("/${env.JOB_BASE_NAME}"))
        )
        println env.JOB_NAME
        println env.JOB_BASE_NAME 
        echo "done reading jobs"

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
      }
    }
    stage('Deploy') {
      steps {
        echo 'Deploy'
      }
    }
  }
  options {
    disableConcurrentBuilds()
    buildDiscarder(logRotator(daysToKeepStr: '50', numToKeepStr: '50'))
    timeout(time: 1, unit: 'HOURS')
    parallelsAlwaysFailFast()
  }
  triggers {
    upstream(
        threshold: hudson.model.Result.SUCCESS, 
        upstreamProjects: 'fakeUpstreamProject/master')
    cron('H 07-19 * * *')
    pollSCM('* * * * *')
  }
}