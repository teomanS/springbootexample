pipeline {
  agent {
    kubernetes {
      yamlFile 'kubepod.yaml'
    }
  }
  stages {
    stage('Run maven') {
      steps {
        container('dindm') {
          sh 'echo MAVEN_CONTAINER_ENV_VAR = ${CONTAINER_ENV_VAR}'
          sh 'ls -al'
          // sh 'dockerd &'
          withCredentials([usernamePassword(credentialsId: 'nexuscred', passwordVariable: 'NEXUS_PASSWORD', usernameVariable: 'NEXUS_USER')]) {
            sh "dockerd && unset MAVEN_CONFIG && cd complete && ./mvnw -s /root/tmp/settings.xml clean && ./mvnw -s /root/tmp/settings.xml spring-boot:build-image -DDOCKER_REGISTRY=nexus-docker-svc.nexus.svc.cluster.local -DDOCKER_REGISTRY_USER=$NEXUS_USER -DDOCKER_REGISTRY_PASSWORD=$NEXUS_PASSWORD"
          }
        }
      }
    }
  }
}