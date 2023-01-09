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
        sh 'docker login -u ravindra45 -p 8618923995'
        sh 'docker tag mytomcat ravindra45/ravindra45:latest'
        sh 'docker push ravindra45/ravindra45:latest'
      }
    }
    stage ('my deploy') {
      agent {label 'deploynode'}
      steps {
        sh 'docker pull ravindra45/ravindra45:latest'
        sh 'docker rm -f mytomcat'
        sh 'docker run -d -p 8080:8080 --name abc ravindra45/ravindra45:latest'
      }
    } 
  }
}
