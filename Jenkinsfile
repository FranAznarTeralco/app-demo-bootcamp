pipeline {

    environment {
        registryBackend = 'franaznarteralco/backend-demo'
        registryFrontend = 'franaznarteralco/frontend-demo'
        registryCredential = 'devcenter-dockerhub'
        NPM_CONFIG_CACHE = "/var/jenkins_home/workspace/.npm"

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
//
//         stage('Build Java Artifact') {
//             steps {
//                 dir(path: '/var/jenkins_home/workspace/app-demo-bootcamp_main/spring-boot-server') {
//                     sh 'mvn -B -DskipTests clean install'
//                 }
//             }
//         }

//         stage('Build Backend image & Push to registry') {
//             steps {
//                 dir(path: '/var/jenkins_home/workspace/app-demo-bootcamp_main/spring-boot-server') {
//                     script {
//                         dockerImage = docker.build registryBackend + ":$BUILD_NUMBER"
//                         docker.withRegistry( '', registryCredential) {
//                             dockerImage.push()
//                         }
//                     }
//                 }
//             }
//         }

        stage('Build NPM Artifact') {
            steps {
                dir(path: '/var/jenkins_home/workspace/app-demo-bootcamp_main/angular-14-client') {
                    sh 'npm install && npm run build'
                }
            }
        }

        stage('Build Frontend image & Push to registry') {
            steps {
                dir(path: '/var/jenkins_home/workspace/app-demo-bootcamp_main/angular-14-client') {
                    script {
                        dockerImage = docker.build registryFrontend + ":$BUILD_NUMBER"
                        docker.withRegistry( '', registryCredential) {
                            dockerImage.push()
                        }
                    }
                }
            }
        }
    }
}