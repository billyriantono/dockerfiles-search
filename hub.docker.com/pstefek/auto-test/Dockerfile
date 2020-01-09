FROM openjdk:8-alpine

RUN mkdir src

WORKDIR ./src

COPY image-automation-test-0.0.1-SNAPSHOT.jar .

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "image-automation-test-0.0.1-SNAPSHOT.jar"]