FROM maven:latest

RUN mkdir -p /opt/groot

WORKDIR /opt/groot

COPY pom.xml .

RUN  mvn dependency:go-offline