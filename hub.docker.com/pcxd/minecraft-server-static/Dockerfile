FROM java:8

MAINTAINER pcxd

ENV APT_GET_UPDATE 2016-04-23
RUN apt-get update

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y \
  imagemagick \
  lsof \
  nano \
  sudo \
  vim \
  jq \
  && apt-get clean

RUN mkdir /data \
  && mkdir /tmp/data \
  && chown bin:bin /data /tmp/data

#ADD https://github.com/itzg/restify/releases/download/1.0.3/restify_linux_amd64 /usr/local/bin/restify
COPY start.sh /start
COPY start-minecraft.sh /start-minecraft
RUN chmod +x /start
RUN chmod +x /start-minecraft
RUN chmod +x /usr/local/bin/*

#VOLUME ["/data","/tmp/data"]
#COPY server.properties /tmp/data/server.properties
#COPY spigot.yml /tmp/data/spigot.yml
WORKDIR /data
#COPY spigot-pixel.jar /tmp/data/
#COPY /plugins /tmp/data/plugins

ENTRYPOINT [ "/start" ]

ENV UID=2 GID=2 \
    MOTD="Play now" \
	RAM_OPTS="-Xmx2048M -Xms1024M" \
    JVM_OPTS="-XX:+UseG1GC -XX:+UnlockExperimentalVMOptions -XX:MaxGCPauseMillis=100 -XX:+DisableExplicitGC -XX:TargetSurvivorRatio=90 -XX:G1NewSizePercent=50 -XX:G1MaxNewSizePercent=80 -XX:InitiatingHeapOccupancyPercent=10 -XX:G1MixedGCLiveThresholdPercent=50 -XX:+AggressiveOpts -XX:+AlwaysPreTouch" \
    TYPE=SPIGOT \
    CONSOLE=false EULA=TRUE TZ=Asia/Bangkok SERVER=spigot_server.jar
