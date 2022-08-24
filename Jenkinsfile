
def customImage = ""

pipeline {

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

    stage('Build Image with Artifact') {
        steps {
            dir(path: '/var/jenkins_home/workspace/app-demo-bootcamp_main/spring-boot-server') {
                customImage = docker.build("franaznarteralco/spring-boot-server:${env.BUILD_ID}")
//                 sh 'docker build -t franaznarteralco/spring-boot-server .'
            }
        }
    }

    stage('Push Backend app image to Registry') {
        steps {
            dir(path: '/var/jenkins_home/workspace/app-demo-bootcamp_main/spring-boot-server') {
                    customImage.push('test')
            }
        }
    }

}

    environment {
        imagename = 'franaznarteralco/backend-demo'
        registryCredential = 'devcenter-dockerhub'
    }

}