FROM openjdk:8-jdk-alpine

EXPOSE 8080


RUN apk add git && git clone https://github.com/Notniws/xml-validator

WORKDIR "/xml-validator"

ENTRYPOINT ["./gradlew", "--console=plain", "--stacktrace", "bootRun"]
