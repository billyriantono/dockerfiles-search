# build stage
FROM gradle:jdk8 AS builder

COPY --chown=gradle:gradle . /home/gradle
RUN ./gradlew clean build --stacktrace

# run stage
FROM gradle:jre-alpine
COPY --from=builder /home/gradle/build/libs/gateway-0.0.1-SNAPSHOT.jar /app/gateway.jar

EXPOSE 8080

CMD ["java", "-jar", "/app/gateway.jar"]
