pipeline {
    environment {
        imagename = 'franaznarteralco/backend-demo'
        registryCredential = 'devcenter-dockerhub'
        dockerImage = ''
    }

    agent {
        docker {
            image 'openjdk:8-jdk-alpine'
            args '-v $HOME/.m2:/root/.m2'
        }
    }

    tools {
        maven "MAVEN"
        jdk "JDK"
    }

    stages {
        stage('Initialize'){
            steps{
                echo "PATH = ${M2_HOME}/bin:${PATH}"
                echo "M2_HOME = /opt/maven"
            }
        }
        stage('Cloning Git') {
            steps {
                git([url: 'https://github.com/FranAznarTeralco/app-demo-bootcamp.git', branch: 'master', credentialsId: 'devcenter-github'])
            }
        }
//         stage('Build') {
//             steps {
//                 dir("/var/lib/jenkins/workspace/spring-boot-angular-14-crud-example/spring-boot-server/jenkins") {
//                     sh 'mvn -B -DskipTests clean install'
//                 }
//             }
//         }
//         stage('Building image') {
//             steps{
//                 script {
//                     dockerImage = docker.build imagename
//                 }
//             }
//         }
//         stage('Deploy Image') {
//                  steps{
//                      script {
//                          docker.withRegistry( '', registryCredential ) {
//                              dockerImage.push("$BUILD_NUMBER")
//                              dockerImage.push('latest')
//                          }
//                      }
//                  }
//              }
//
//         stage('Remove Unused docker image') {
//             steps{
//                 sh "docker rmi $imagename:$BUILD_NUMBER"
//                 sh "docker rmi $imagename:latest"
//             }
//         }

     }

//     post {
//        always {
//           junit(
//             allowEmptyResults: true,
//             testResults: '*/test-reports/.xml'
//           )
//        }
//     }
}
