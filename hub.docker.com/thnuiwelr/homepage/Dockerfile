FROM openjdk:8u171-jdk-alpine3.8 as builder

ADD . /app/server
WORKDIR /app/server

RUN chmod +x ./gradlew && \
    ./gradlew :shadowJar && \
    mv build/libs/server-1.jar /server.jar

FROM openjdk:8u171-jre-alpine3.8 as environment
WORKDIR /app
COPY --from=builder /server.jar .
CMD java -jar /app/server.jar