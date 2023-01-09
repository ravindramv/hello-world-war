pipeline {
  agent {label 'firstnode'}
  stages {
    stage ('my build') {
      steps {
        sh "echo ${BUILD_VERSION}"
        sh "docker build -t mytomcat ."
      }
    }
    stage ('publish stage') {
      steps {
        sh "echo ${BUILD_VERSION}"
        sh 'docker login -u ravindramv -p 8618923995'
        sh 'docker tag mytomcat:latest ravindra45/ravindra45:latest'
        sh 'docker push ravindra45/ravindra45'
      }
    }
    stage ('my deploy') {
      agent {label 'deploynode'}
      steps {
        sh 'docker pull ravindra45/ravindra45:latest'
        sh 'docker rm -f mytomcat'
        sh ' run -d -p 8888:8080 --name ravindra ravindra45/ravindra45:latest'
      }
    } 
  }
}
