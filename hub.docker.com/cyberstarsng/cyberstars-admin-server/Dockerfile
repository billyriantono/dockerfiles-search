FROM maven:3.6-jdk-8-alpine AS builder
WORKDIR /app
COPY pom.xml .
RUN mvn -e -B dependency:resolve
COPY src ./src
RUN mvn -e -B package -DskipTests

FROM openjdk:8-jdk-alpine
LABEL maintaner="cyberstarsng@gmail.com"
VOLUME /opt/admin-server
EXPOSE 8001
COPY --from=builder /app/target/cyberstars-admin-server.jar /
CMD ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/cyberstars-admin-server.jar"]
