# FROM openjdk:8-jdk-alpine

# COPY ./target/ads-*.jar app.jar

# ENTRYPOINT ["java", "-jar", "/app.jar", ""]

FROM maven:3.6.0-jdk-11-slim AS build
COPY src /home/app/src
COPY pom.xml /home/app
RUN mvn -f /home/app/pom.xml clean package

FROM openjdk:11-jre-slim
COPY --from=build /home/app/target/ads-*.jar /usr/local/lib/app.jar
EXPOSE 8091
ENTRYPOINT ["java","-jar","/usr/local/lib/app.jar"]
