FROM openjdk:alpine
LABEL maintainer "Nekroido"

VOLUME [ "/minecraft/world", "/minecraft/logs", "/minecraft/config", "/minecraft/mods", "/minecraft/merge" ]

# Minecraft server, RCON, Dynmap and JourneyMap
EXPOSE 25565 25575 8123 8080

WORKDIR /minecraft

CMD [ "./etc/scripts/bootstrap" ]

ENV MODPACK_MANIFEST_URL ""
ENV CURSE_MODPACK_ID ""

ENV MINECRAFT_VERSION 1.12.2
ENV FORGE_VERSION 14.23.5.2838

ENV MINECRAFT_JAR minecraft_server.${MINECRAFT_VERSION}.jar
ENV MINECRAFT_URL https://s3.amazonaws.com/Minecraft.Download/versions/${MINECRAFT_VERSION}/${MINECRAFT_JAR}

ENV FORGE_JAR forge-${MINECRAFT_VERSION}-${FORGE_VERSION}-universal.jar
ENV FORGE_URL http://files.minecraftforge.net/maven/net/minecraftforge/forge/${MINECRAFT_VERSION}-${FORGE_VERSION}/forge-${MINECRAFT_VERSION}-${FORGE_VERSION}-installer.jar

# Download cURL, bash, unzip and jq
RUN apk --no-cache -U add curl bash unzip jq

RUN echo /minecraft/${MINECRAFT_JAR}
# Download Minecraft server
RUN curl -sLO ${MINECRAFT_URL}

# Download and install Forge
RUN curl -sLO ${FORGE_URL} && \
  cd /minecraft && \
  java -jar forge-${MINECRAFT_VERSION}-${FORGE_VERSION}-installer.jar --installServer && \
  rm -f /minecraft/forge-${MINECRAFT_VERSION}-${FORGE_VERSION}-installer.jar /minecraft/forge-${MINECRAFT_VERSION}-${FORGE_VERSION}-installer.jar.log

ADD scripts ./etc/scripts

ARG VERSION
ARG BUILD_DATE
ARG VCS_REF

LABEL org.label-schema.version=$VERSION
LABEL org.label-schema.build-date=$BUILD_DATE
LABEL org.label-schema.vcs-ref=$VCS_REF
