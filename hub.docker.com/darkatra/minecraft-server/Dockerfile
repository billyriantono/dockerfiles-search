FROM openjdk:8-jre-alpine

MAINTAINER DarkAtra <darkatra@web.de>

ENV DOWNLOAD_URL https://launcher.mojang.com/v1/objects/f1a0073671057f01aa843443fef34330281333ce/server.jar

RUN apk add curl; \
    curl -o /server.jar ${DOWNLOAD_URL}

WORKDIR /data
VOLUME /data
EXPOSE 25565

CMD echo eula=true > /data/eula.txt && java -Xmx1024M -Xms1024M -jar /server.jar nogui