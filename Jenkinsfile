pipeline {
  agent any
  stages {
    stage('Initialize') {
      steps {
        sh '''echo "PATH = ${M2_HOME}/bin:${PATH}"
echo "M2_HOME = /opt/maven"'''
      }
    }

    stage('Cloning Git') {
      steps {
        git(url: 'https://github.com/FranAznarTeralco/app-demo-bootcamp.git', branch: 'main', credentialsId: 'GitHubCredentials')
      }
    }

    stage('Build') {
      steps {
        sh '''cd /var/lib/jenkins/workspace/spring-boot-angular-14-crud-example/spring-boot-server/jenkins
&& sh \'mvn -B -DskipTests clean install\''''
      }
    }

    stage('Build Docker Image') {
      steps {
        dockerNode(image: 'openjdk:8-jdk-alpine')
      }
    }

  }
  environment {
    imagename = 'franaznarteralco/backend-demo'
    registryCredential = 'devcenter-dockerhub'
    dockerImage = ''
  }
}