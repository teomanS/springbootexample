pipeline {
  agent {
    kubernetes {
      yamlFile 'kubepod.yaml'
    }
  }
  stages {
    stage('Run maven') {
      steps {
        container('maven') {
          sh 'echo MAVEN_CONTAINER_ENV_VAR = ${CONTAINER_ENV_VAR}'
          sh 'ls -al'
        }
      }
    }
  }
}