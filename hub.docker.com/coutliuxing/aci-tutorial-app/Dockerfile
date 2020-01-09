FROM openjdk:8-jdk-alpine
VOLUME /tmp
ADD /target/spring-boot-docker-1.0.jar app.jar
ADD 214297831890270.pfx 214297831890270.pfx

RUN mvn clean package

ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/app.jar"]