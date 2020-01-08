FROM maven:3-jdk-11-slim AS maven
WORKDIR /app
RUN mkdir -p /app
COPY pom.xml ./pom.xml
RUN mvn -q -B -e -C -T 1C dependency:go-offline
COPY src ./src
RUN mvn -q -B -e -C -T 1C verify

FROM openjdk:11-jdk-slim
WORKDIR /app
ENTRYPOINT ["java", "-jar", "app.jar"]
COPY --from=maven /app/target/app.jar /app/app.jar