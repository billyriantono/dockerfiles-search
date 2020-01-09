FROM maven:3.5.2-jdk-8-alpine AS MAVEN_TOOL_CHAIN

COPY pom.xml /tmp/
COPY src /tmp/src/

WORKDIR /tmp/

RUN mvn package

FROM openjdk:8-jdk-alpine

COPY --from=MAVEN_TOOL_CHAIN /tmp/target/retail-store-api-1.0.0.jar /usr/src/retail-store-api-1.0.0.jar

CMD java -Dspring.profiles.active=docker -jar /usr/src/retail-store-api-1.0.0.jar