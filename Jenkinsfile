pipeline {
  agent {label 'slave1'}
  stages {
    stage ('my build') {
      steps {
        sh "echo ${BUILD_VERSION}"
        sh "docker build -t mytomcat ."
        sh 'helm package ./helm/tomcat --version=${BUILD_NUMBER}'
      }
    }
    stage ('publish stage') {
      steps {
        sh "echo ${BUILD_VERSION}"
        withCredentials([usernamePassword(credentialsId: 'Dockerhub', passwordVariable: 'DockerhubPassword', usernameVariable: 'DockerhubUser')]) {
        sh "docker login -u ${env.DockerhubUser} -p ${env.DockerhubPassword}"
        sh 'docker tag mytomcat ravindra45/ravindra45:${BUILD_VERSION}'
        sh 'docker push ravindra45/ravindra45:${BUILD_VERSION}'
          
        sh 'curl -uravindramv110296@gmail.com:Ravindramv45110296@ -T tomcat-${BUILD_NUMBER}.tgz \"https://jfrogforhelm.jfrog.io/artifactory/helm/tomcat-${BUILD_NUMBER}.tgz\"'  
        }  
      }
    }
    stage ('my deploy') {
      agent {label 'helm'}
      steps {
        sh 'helm repo add helm https://jfrogforhelm.jfrog.io/artifactory/api/helm/helm --username ravindramv110296@gmail.com --password Ravindramv45110296@'
        sh 'helm repo update'
        sh 'helm repo list'
        sh 'helm upgrade --install mytomcat helm/tomcat --version=${BUILD_NUMBER} --set selector_label=tomcat --set deployment_name=tomcat --set replicas=2 --set registry_name=ravindra45 --set docker_repo_name=ravindra45 --set image_tag=${BUILD_NUMBER} --set port_name=tomcat --set target_port=8080 --set port=8080'
      }
    } 
  }
}
