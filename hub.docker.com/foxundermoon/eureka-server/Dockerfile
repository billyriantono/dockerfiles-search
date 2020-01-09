
FROM gradle as builder

COPY --chown=gradle:gradle . /home/gradle/src
WORKDIR /home/gradle/src
RUN gradle bootJar

FROM openjdk:8-jdk
EXPOSE 8761
COPY --from=builder /home/gradle/src/build/libs/eureka-server-0.0.1.jar /app/
WORKDIR /app
CMD java -jar /app/eureka-server-0.0.1.jar



