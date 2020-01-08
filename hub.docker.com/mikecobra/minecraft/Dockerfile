FROM alpine:3.3

MAINTAINER Mike Clarke <michaelclarkecs@gmail.com>

RUN apk --update add openjdk8-jre && rm -rf /var/cache/apk/*
RUN addgroup minecraft && adduser -s /bin/ash -G minecraft -D minecraft

VOLUME /minecraft
WORKDIR /minecraft
EXPOSE 25565
USER minecraft

ENTRYPOINT ["java", "-jar", "/minecraft_server.jar", "nogui"]
