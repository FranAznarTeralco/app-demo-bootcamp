
pipeline {

    environment {
        imagename = 'franaznarteralco/backend-demo'
        registryCredential = 'devcenter-dockerhub'
    }

    agent any

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

    stage('Build Java Artifact') {
        steps {
            dir(path: '/var/jenkins_home/workspace/app-demo-bootcamp_main/spring-boot-server') {
                sh 'mvn -B -DskipTests clean install'
            }
        }
    }

    stage('Build image with Java artifact') {
        steps {
            dir(path: '/var/jenkins_home/workspace/app-demo-bootcamp_main/spring-boot-server') {
              sh 'docker build -t franaznarteralco/spring-boot-server:test-' + ${env.BUILD_ID} + ' .'
            }
        }
    }

    stage('Deploy Image') {
        steps{
            script {
                docker.withRegistry( '', registryCredential) {
                    dockerImage.push()
                }
            }
        }
    }

}

}