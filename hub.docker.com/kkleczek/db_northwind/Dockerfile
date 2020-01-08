FROM maven:3.5-jdk-8 AS build
WORKDIR /nortwind-api
COPY . .
RUN mvn -f demo/pom.xml -U clean package


FROM openjdk:8-jdk-alpine
EXPOSE 8080
COPY --from=build /nortwind-api/demo/target/demo-0.0.1-SNAPSHOT.jar /
CMD ["java", "-jar", "/demo-0.0.1-SNAPSHOT.jar", "-Dspring.datasource.url=jdbc:postgresql://database:5432/northwind"]