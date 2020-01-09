#
# Docker file for Spring Boot Admin
#
FROM maven:3.3.9-jdk-8-alpine
MAINTAINER Merapar

ENV TZ UTC

RUN     mkdir -p /usr/src/app
WORKDIR /usr/src/app
ADD     . /usr/src/app
RUN     mvn package && cp target/*.jar /usr/src/app/spring-boot-admin.jar

CMD ["java", "-XX:MinHeapFreeRatio=10", "-XX:MaxHeapFreeRatio=10", "-Xms10m", "-jar", "spring-boot-admin.jar" ]