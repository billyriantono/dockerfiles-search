FROM maven:3.5-jdk-8-alpine as maven
WORKDIR /app
COPY ./ /app
RUN mvn install

FROM openjdk:alpine
# This command not working now
#ADD /target/demo-docker-1.0.jar demo-docker-1.0.jar
COPY --from=maven /app/target/demo-docker-1.0.jar demo-docker-1.0.jar
ENTRYPOINT ["java", "-jar", "demo-docker-1.0.jar"]