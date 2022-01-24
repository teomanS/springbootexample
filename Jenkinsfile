pipeline {
  agent {
    kubernetes {
      yamlFile 'kubepod.yaml'
    }
  }
  /*
  stages {
    stage('SonarCloud') {
      environment {
        SCANNER_HOME = tool 'SonarQubeScanner'
        ORGANIZATION = "exampleorg"
        PROJECT_NAME = "springbootexample"
      }
      steps {
        withSonarQubeEnv('SonarQubeScanner') {
            sh '''$SCANNER_HOME/bin/sonar-scanner -Dsonar.organization=$ORGANIZATION \
            -Dsonar.java.binaries=build/classes/java/ \
            -Dsonar.projectKey=$PROJECT_NAME \
            -Dsonar.sources=.'''
        }
      }
    }
    */    
    stage('Run maven') {
      steps {
        container('maven') {
          sh 'echo MAVEN_CONTAINER_ENV_VAR = ${CONTAINER_ENV_VAR}'
          sh 'ls -al'
          // sh 'dockerd &'
          withCredentials([usernamePassword(credentialsId: 'dockerreg', passwordVariable: 'NEXUS_PASSWORD', usernameVariable: 'NEXUS_USER')]) {
            sh "unset MAVEN_CONFIG && cd complete && ./mvnw -s /root/tmp/settings.xml clean && ./mvnw -s /root/tmp/settings.xml spring-boot:build-image -DDOCKER_REGISTRY=teopocregistery.azurecr.io -DDOCKER_REGISTRY_USER=$NEXUS_USER -DDOCKER_REGISTRY_PASSWORD=$NEXUS_PASSWORD"
          }
        }
      }
    }
  }
}