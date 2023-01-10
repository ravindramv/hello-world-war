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
        withCredentials([usernamePassword(credentialsId: 'Dockerhub', passwordVariable: 'DockerhubPassword', usernameVariable: 'DockerhubUser')]) {
        sh "docker login -u ${env.DockerhubUser} -p ${env.DockerhubPassword}"
        sh 'docker tag mytomcat ravindra45/ravindra45:${BUILD_VERSION}'
        sh 'docker push ravindra45/ravindra45:${BUILD_VERSION}'
        }  
      }
    }
    stage ('my deploy') {
      agent {label 'deploynode'}
      steps {
        sh 'docker pull ravindra45/ravindra45:${BUILD_VERSION}'
        sh 'docker rm -f mytomcat'
        sh 'docker run -d -p 8085:8080 --name abc ravindra45/ravindra45:${BUILD_VERSION}'
      }
    } 
  }
}
