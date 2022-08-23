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
        git(url: 'https://github.com/FranAznarTeralco/app-demo-bootcamp.git', branch: 'main', changelog: true, credentialsId: 'devcenter-github', poll: true)
      }
    }

    stage('Build') {
      steps {
        dir(path: '/var/jenkins_home/workspace/app-demo-bootcamp_main/spring-boot-server/jenkins') {
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