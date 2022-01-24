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
          sh 'dockerd &'
          
          sh " unset MAVEN_CONFIG && cd complete && ./mvnw -s /root/tmp/settings.xml clean && ./mvnw -s /root/tmp/settings.xml spring-boot:build-image"
        }
      }
    }
  }
}