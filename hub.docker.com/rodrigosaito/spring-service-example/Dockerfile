FROM openjdk:12-jdk-alpine

WORKDIR /app
COPY . /app

RUN ./mvnw clean package

FROM openjdk:12-alpine

WORKDIR /app
COPY --from=0 /app/target/spring-service-example-1.0-SNAPSHOT.jar /app/spring-service-example.jar

EXPOSE 8080

CMD ["java", "-jar", "spring-service-example.jar"]