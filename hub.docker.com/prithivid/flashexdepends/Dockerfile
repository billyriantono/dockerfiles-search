FROM maven:3.6-jdk-11

COPY / /dependencies

WORKDIR /dependencies

RUN mvn dependency:go-offline
