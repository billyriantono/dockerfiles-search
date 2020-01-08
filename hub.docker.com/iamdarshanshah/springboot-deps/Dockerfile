FROM maven:3.6.0-jdk-12-alpine

COPY / /deps

WORKDIR /deps

RUN mvn dependency:go-offline