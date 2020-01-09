FROM openjdk:8-jdk-alpine

LABEL maintainer="Ansel Corona <anselcorona@gmail.com>"

EXPOSE 8080

COPY correo-0.0.1-SNAPSHOT.jar finalcorreo.jar

ENTRYPOINT ["java", "-jar", "finalcorreo.jar"]
