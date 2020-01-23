FROM gradle:4.2.1-jdk8 AS build
MAINTAINER bandoshintaro<bando142141@gmail.com>

USER root
COPY ./build.gradle netapp-dummy/
COPY ./src netapp-dummy/src
WORKDIR netapp-dummy
RUN gradle build -x test

FROM java:openjdk-8-jre-alpine
COPY --from=build /home/gradle/netapp-dummy/build/libs/netapp-dummy-0.0.1.jar /

ENTRYPOINT ["java", "-jar", "/netapp-dummy-0.0.1.jar"]

EXPOSE 8080