FROM alpine:latest

LABEL maintainer="Mihoko-Okayami (https://hub.docker.com/r/mihokookayami/minecraft/)"

ARG XMS=1G
ARG XMX=1G
ENV XMS "$XMS"
ENV XMX "$XMX"

RUN apk add --no-cache openjdk8

EXPOSE 25565 25575

WORKDIR /data

CMD java -Xms$XMS -Xmx$XMX -XX:+UseConcMarkSweepGC -jar server.jar
