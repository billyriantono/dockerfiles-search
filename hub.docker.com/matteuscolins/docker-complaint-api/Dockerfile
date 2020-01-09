FROM openjdk:8-alpine

MAINTAINER Matteus Colins

RUN apk update && apk add bash

RUN mkdir -p /opt/app

ENV PROJECT_HOME /opt/app

COPY target/complaint-api-0.0.1-SNAPSHOT.jar $PROJECT_HOME/complaint-api.jar

WORKDIR $PROJECT_HOME

CMD ["java", "-jar", "-Dspring.profiles.active=prod" ,"./complaint-api.jar"]