FROM gradle:6.0.1-jdk11 as builder

USER root
COPY . .
RUN gradle build -i
RUN chmod +x ./docker/flash-http-gateway/flash-http-gateway.sh


FROM openjdk:11.0.5-slim

WORKDIR /flash

EXPOSE 8080

COPY --from=builder /home/gradle/build/libs/*-all.jar /flash/flash.jar
COPY --from=builder /home/gradle/docker/flash-http-gateway/flash-http-gateway.sh /flash/flash-http-gateway.sh

ENV MONGO_URI      mongodb://mongo:27017/flash
ENV MONGO_DATABASE flash

ENTRYPOINT [ "/flash/flash-http-gateway.sh" ]
