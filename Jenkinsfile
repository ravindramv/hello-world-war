pipeline {
  agent {label 'firstnode'}
  stages {
    stage ('my build') {
      steps {
        sh 'sudo mvn package'
        sh 'ls'
        sh 'scp -R target/slave@172.31.45.224:/opt/tomcat/webapps'
      }
    }
    stage ('my deploy') {
      agent {label 'slave'}
      steps {
      sh 'sudo sh /opt/tomcat/bin/shutdown.sh'
      sh 'sleep 2'
      sh 'sudo sh /opt/tomcat/bin/startup.sh'
      }
    } 
  }
}
