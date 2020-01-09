FROM maven:3.6-jdk-8-alpine AS builder
WORKDIR /app
COPY pom.xml .
RUN mvn -e -B dependency:resolve
COPY src ./src
RUN mvn -e -B package -DskipTests

FROM openjdk:8-jdk-alpine
LABEL maintaner="cyberstarsng@gmail.com"
VOLUME /opt/payment-service
EXPOSE 8005
COPY --from=builder /app/target/cyberstars-payment-service.jar /
CMD ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/cyberstars-payment-service.jar"]
