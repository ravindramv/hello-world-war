pipeline {
  agent {label 'firstnode'}
  stages {
    stage ('my build') {
      steps {
        sh 'maven package'
        sh 'ls'
        
      }
    }
  }
}
