FROM gradle:5.5.0-jdk8 as builder
COPY --chown=gradle:gradle . /home/gradle/src
WORKDIR /home/gradle/src
RUN gradle build customFatJar

FROM openjdk:8-alpine
EXPOSE 4444
COPY --from=builder /home/gradle/src/build/libs/sopra1920_server.jar /app/
WORKDIR /app
CMD ["java", "-jar", "sopra1920_server.jar"]