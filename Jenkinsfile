pipeline {
  agent any
  stages {
    stage('find upstream job') {
      steps {
        script {
          def upstreamBuilds = currentBuild.getUpstreamBuilds()
          for(upstreamBuild in upstreamBuilds) {
            println '\t \t upstreamBuild.getClass(); --- ' + upstreamBuild.getClass();
            println '\t \t upstreamBuild.hashCode();  --- ' + upstreamBuild.hashCode(); 
            println '\t \t upstreamBuild.toString(); --- ' + upstreamBuild.toString();
            println '\t \t upstreamBuild.getAbsoluteUrl();  --- ' + upstreamBuild.getAbsoluteUrl(); 
            println '\t \t upstreamBuild.getBuildCauses();  --- ' + upstreamBuild.getBuildCauses(); 
            println '\t \t upstreamBuild.getBuildVariables();  --- ' + upstreamBuild.getBuildVariables(); 
            println '\t \t upstreamBuild.getChangeSets();  --- ' + upstreamBuild.getChangeSets(); 
            println '\t \t upstreamBuild.getCurrentResult();  --- ' + upstreamBuild.getCurrentResult(); 
            println '\t \t upstreamBuild.getDescription();  --- ' + upstreamBuild.getDescription(); 
            println '\t \t upstreamBuild.getDisplayName(); --- ' + upstreamBuild.getDisplayName();
            println '\t \t upstreamBuild.getDuration();  --- ' + upstreamBuild.getDuration(); 
            println '\t \t upstreamBuild.getDurationString(); --- ' + upstreamBuild.getDurationString();
            println '\t \t upstreamBuild.getFullDisplayName();  --- ' + upstreamBuild.getFullDisplayName(); 
            println '\t \t upstreamBuild.getFullProjectName(); --- ' + upstreamBuild.getFullProjectName();
            println '\t \t upstreamBuild.getId();  --- ' + upstreamBuild.getId(); 
            println '\t \t upstreamBuild.getNextBuild(); --- ' + upstreamBuild.getNextBuild();
            println '\t \t upstreamBuild.getNumber(); --- ' + upstreamBuild.getNumber();
            println '\t \t upstreamBuild.getPreviousBuild(); --- ' + upstreamBuild.getPreviousBuild();
            println '\t \t upstreamBuild.getProjectName();  --- ' + upstreamBuild.getProjectName(); 
            println '\t \t upstreamBuild.getRawBuild();  --- ' + upstreamBuild.getRawBuild(); 
            println '\t \t upstreamBuild.getResult();  --- ' + upstreamBuild.getResult(); 
            println '\t \t upstreamBuild.getStartTimeInMillis();  --- ' + upstreamBuild.getStartTimeInMillis(); 
            println '\t \t upstreamBuild.getTimeInMillis();  --- ' + upstreamBuild.getTimeInMillis(); 
            println '\t \t upstreamBuild.getUpstreamBuilds();  --- ' + upstreamBuild.getUpstreamBuilds(); 

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
    upstream(threshold: hudson.model.Result.SUCCESS, upstreamProjects: "fakeUpstreamProject/" + env.BRANCH_NAME.replaceAll("/", "%2F")) 
    cron('H 07-19 * * *')
    pollSCM('* * * * *')
  }
}