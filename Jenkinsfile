pipeline {
  agent any
  stages {
    stage('find upstream job') {
      steps {
        script {
          def upstreamBuilds = currentBuild.getUpstreamBuilds()
          for(upstreamBuild in upstreamBuilds) {
            println "1) upstreamBuild.toString() " + upstreamBuild.toString()
            println "2) upstreamBuild.toString() : " + upstreamBuild.toString()
            println "3) upstreamBuild.getProjectName() : " + upstreamBuild.getProjectName()
            println "4) upstreamBuild : " + upstreamBuild


            if( !upstreamBuild ){
              println( "Object is null\r\n" );
              return;
            }
            if( !upstreamBuild.metaClass && upstreamBuild.getClass() ){
              printAllMethods( upstreamBuild.getClass() );
              return;
            }
            def str = "class ${upstreamBuild.getClass().name} functions:\r\n";
            upstreamBuild.metaClass.methods.name.unique().each{
              str += it+"(); ";
            }
            println "${str}\r\n";


          }
        }

      }
    }
    stage('Build') {
      parallel {
        stage('Build Stage 1') {
          steps {
            echo 'Stage #1'
          }
        }
        stage('Build Stage 2') {
          steps {
            echo 'Stage #2'
          }
        }
        stage('Build Stage 3') {
          steps {
            echo 'Stage #3'
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
    upstream(threshold: hudson.model.Result.SUCCESS, upstreamProjects: "fakeUpstreamProject/" + env.BRANCH_NAME.replaceAll("/", "%2F") 
    cron('H 07-19 * * *')
    pollSCM('* * * * *')
  }
}