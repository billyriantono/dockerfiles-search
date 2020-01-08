FROM alpine:latest
RUN echo "http://dl-4.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories \
 && apk add --update openjdk8-jre-base && rm -rf /var/cache/apk/*
RUN apk add curl jq
RUN mkdir /mc
WORKDIR /mc
RUN wget -q $(curl -s $(curl -s https://launchermeta.mojang.com/mc/game/version_manifest.json | jq -r ".versions[] | select(.id == $(curl -s https://launchermeta.mojang.com/mc/game/version_manifest.json | jq .latest.snapshot)) .url") | jq -r .downloads.server.url) -O /mc/server.jar
VOLUME [ "/mc/world" ]
CMD ["/usr/bin/java","-Xms2048M","-Xmx12288M","-jar","/mc/server.jar","nogui"]
