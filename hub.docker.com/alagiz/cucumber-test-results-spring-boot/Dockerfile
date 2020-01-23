FROM maven:3.5-jdk-8 as BUILD

COPY /komkommer-spring-boot/src /usr/src/komkommer-spring-boot/src
COPY /komkommer-spring-boot/pom.xml /usr/src/komkommer-spring-boot

RUN mvn -f /usr/src/komkommer-spring-boot/pom.xml install

FROM openjdk:8

COPY --from=BUILD /usr/src/komkommer-spring-boot/target/*.jar  /app.jar