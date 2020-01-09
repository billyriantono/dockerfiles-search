FROM java:8-jdk-alpine
MAINTAINER lalala

ADD . /app
WORKDIR /app
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "demo1-2.0.1-SNAPSHOT.jar", "--spring.profiles.active=test"]