pipeline {
  agent {label 'firstnode'}
  stages {
    stage ('my build') {
      steps {
        sh 'sudo mvn package'
        sh 'ls'
        sh 'scp -R target/hello-world-war-1.0.0.war devops@172.31.38.254:/opt/tomcat/webapps'
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
