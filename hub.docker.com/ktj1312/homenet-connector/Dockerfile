FROM openjdk:8-jdk-alpine
MAINTAINER Tac Jin Kim <ktj1312@gwnu.ac.kr>

VOLUME /tmp
EXPOSE 8080

ARG JAR_FILE
COPY ${JAR_FILE} app.jar
ENTRYPOINT ["java","-jar","/app.jar"]