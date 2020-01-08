FROM openjdk:8-jdk-alpine
RUN apk update && apk add bash
VOLUME /tmp
ADD vapp_szalek-1.0.jar vapp_szalek-1.0.jar
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/vapp_szalek-1.0.jar"]
EXPOSE 8080