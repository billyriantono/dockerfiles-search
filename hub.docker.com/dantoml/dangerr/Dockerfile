FROM maven:3.5.4-jdk-8-alpine AS build  
COPY src /usr/src/app/src  
COPY pom.xml /usr/src/app  
RUN mvn -f /usr/src/app/pom.xml clean package

FROM solsson/kafka:0.11.0.0
COPY config/connect-ethereum-source.properties config/
COPY config/connect-standalone.properties config/
COPY --from=build /usr/src/app/target/kafka-ethereum-connector-1.0.jar /opt/kafka/libs/

ENTRYPOINT ["./bin/connect-standalone.sh", "config/connect-standalone.properties", "config/connect-ethereum-source.properties"]