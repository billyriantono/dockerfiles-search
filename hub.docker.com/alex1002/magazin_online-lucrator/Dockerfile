FROM maven:3.5-jdk-8-alpine AS build
WORKDIR /aplicatie
ADD pom.xml .
RUN ["mvn", "dependency:resolve"]
RUN ["mvn", "verify"]
ADD "src/main" "./src/main"
RUN ["mvn", "package"]

FROM openjdk:8-jre-alpine
COPY --from=build /aplicatie/target/lucrator-jar-with-dependencies.jar /
CMD ["java", "-XX:+UnlockExperimentalVMOptions", "-XX:+UseCGroupMemoryLimitForHeap", "-jar", "/lucrator-jar-with-dependencies.jar"]
