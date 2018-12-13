pipeline {
  agent any
  stages {
    stage('find upstream job') {
      steps {
        script {
          def upstreamBuilds = currentBuild.getUpstreamBuilds()
          for(upstreamBuild in upstreamBuilds) {
            println 'upstreamBuild.equals();  --- ' + upstreamBuild.equals(); 
            println 'upstreamBuild.getClass(); --- ' + upstreamBuild.getClass();
            println 'upstreamBuild.hashCode();  --- ' + upstreamBuild.hashCode(); 
            println 'upstreamBuild.notify();  --- ' + upstreamBuild.notify(); 
            println 'upstreamBuild.notifyAll(); --- ' + upstreamBuild.notifyAll();
            println 'upstreamBuild.toString(); --- ' + upstreamBuild.toString();
            println 'upstreamBuild.wait();  --- ' + upstreamBuild.wait(); 
            println 'upstreamBuild.getAbsoluteUrl();  --- ' + upstreamBuild.getAbsoluteUrl(); 
            println 'upstreamBuild.getBuildCauses();  --- ' + upstreamBuild.getBuildCauses(); 
            println 'upstreamBuild.getBuildVariables();  --- ' + upstreamBuild.getBuildVariables(); 
            println 'upstreamBuild.getChangeSets();  --- ' + upstreamBuild.getChangeSets(); 
            println 'upstreamBuild.getCurrentResult();  --- ' + upstreamBuild.getCurrentResult(); 
            println 'upstreamBuild.getDescription();  --- ' + upstreamBuild.getDescription(); 
            println 'upstreamBuild.getDisplayName(); --- ' + upstreamBuild.getDisplayName();
            println 'upstreamBuild.getDuration();  --- ' + upstreamBuild.getDuration(); 
            println 'upstreamBuild.getDurationString(); --- ' + upstreamBuild.getDurationString();
            println 'upstreamBuild.getFullDisplayName();  --- ' + upstreamBuild.getFullDisplayName(); 
            println 'upstreamBuild.getFullProjectName(); --- ' + upstreamBuild.getFullProjectName();
            println 'upstreamBuild.getId();  --- ' + upstreamBuild.getId(); 
            println 'upstreamBuild.getNextBuild(); --- ' + upstreamBuild.getNextBuild();
            println 'upstreamBuild.getNumber(); --- ' + upstreamBuild.getNumber();
            println 'upstreamBuild.getPreviousBuild(); --- ' + upstreamBuild.getPreviousBuild();
            println 'upstreamBuild.getProjectName();  --- ' + upstreamBuild.getProjectName(); 
            println 'upstreamBuild.getRawBuild();  --- ' + upstreamBuild.getRawBuild(); 
            println 'upstreamBuild.getResult();  --- ' + upstreamBuild.getResult(); 
            println 'upstreamBuild.getStartTimeInMillis();  --- ' + upstreamBuild.getStartTimeInMillis(); 
            println 'upstreamBuild.getTimeInMillis();  --- ' + upstreamBuild.getTimeInMillis(); 
            println 'upstreamBuild.getUpstreamBuilds();  --- ' + upstreamBuild.getUpstreamBuilds(); 
            println 'upstreamBuild.isKeepLog();  --- ' + upstreamBuild.isKeepLog(); 
            println 'upstreamBuild.resultIsBetterOrEqualTo();  --- ' + upstreamBuild.resultIsBetterOrEqualTo(); 
            println 'upstreamBuild.resultIsWorseOrEqualTo();  --- ' + upstreamBuild.resultIsWorseOrEqualTo(); 
            println 'upstreamBuild.setDescription();  --- ' + upstreamBuild.setDescription(); 
            println 'upstreamBuild.setDisplayName();  --- ' + upstreamBuild.setDisplayName(); 
            println 'upstreamBuild.setKeepLog();  --- ' + upstreamBuild.setKeepLog(); 
            println 'upstreamBuild.setResult(); --- ' + upstreamBuild.setResult();

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