pipeline {
  agent {label 'firstnode'}
  stages {
    stage ('my build') {
      steps {
        sh 'mvn package'
        sh 'ls'
      }
    }
    stage ('my deploy') {
      steps {
      sh 'sudo cp -R target/hello-world-war-1.0.0.war /opt/tomcat/webapps/'
      sh 'sudo sh /opt/tomcat/bin/shutdown.sh'
      sh 'sleep 2'
      sh 'sudo sh /opt/tomcat/bin/startup.sh'
      }
    } 
  }
}
