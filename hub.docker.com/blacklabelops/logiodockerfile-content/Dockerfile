FROM openjdk:8 as builder
MAINTAINER Balkrishna Pandey
WORKDIR /app

COPY . .
RUN ./gradlew build

FROM openjdk:8-jdk-alpine
COPY --from=builder /app/build/libs/*.jar  /app.jar
EXPOSE 8080
ENTRYPOINT [ "java", "-jar", "/app.jar" ]