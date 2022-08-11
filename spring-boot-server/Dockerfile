FROM openjdk:8-jdk-alpine

ARG JAR_FILE=target/*.jar
COPY ${JAR_FILE} spring-boot-jpa-h2-0.0.1-SNAPSHOT.jar

EXPOSE 8080
ENTRYPOINT ["java","-jar","/spring-boot-jpa-h2-0.0.1-SNAPSHOT.jar"]