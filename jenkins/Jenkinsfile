pipeline {
  agent {
    docker {
      image 'openjdk:8-jdk-alpine'
      args '-v $HOME/.m2:/root/.m2'
    }

  }
  stages {
    stage('Initialize Maven') {
      steps {
        sh 'echo "PATH = ${M2_HOME}/bin:${PATH}" && echo "M2_HOME = /opt/maven"'
      }
    }

    stage('Cloning Git') {
      steps {
        git(url: 'https://github.com/FranAznarTeralco/app-demo-bootcamp.git', branch: 'master', credentialsId: 'devcenter-github')
      }
    }

    stage('Build') {
      steps {
        dir(path: '/var/lib/jenkins/workspace/spring-boot-angular-14-crud-example/spring-boot-server/jenkins') {
          sh 'mvn -B -DskipTests clean install'
        }

      }
    }

  }
  environment {
    imagename = 'franaznarteralco/backend-demo'
    registryCredential = 'devcenter-dockerhub'
  }
}