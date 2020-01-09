FROM maven:3.5-jdk-8-alpine as maven
WORKDIR /app
COPY ./ /app
RUN mvn install


FROM openjdk:alpine
COPY --from=maven /app/target/soap-service-1.0.jar soap-service-1.0.jar
ENTRYPOINT ["java", "-jar", "soap-service-1.0.jar"]