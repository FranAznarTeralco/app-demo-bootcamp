
pipeline {

    environment {
        registry = 'franaznarteralco/backend-demo'
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

        stage('Build image & Push to registry') {
            steps {
                dir(path: '/var/jenkins_home/workspace/app-demo-bootcamp_main/spring-boot-server') {
                    script {
                        docker.build registry + ":$BUILD_NUMBER"
                        docker.withRegistry( '', registryCredential) {
                            dockerImage.push()
                        }
                    }
                }
            }
        }
    }
}