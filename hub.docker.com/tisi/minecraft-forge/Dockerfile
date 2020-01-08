FROM tisi/minecraft-vanilla:latest
MAINTAINER Desnoo

VOLUME ["/minecraft/merge", "/minecraft/world", "/minecraft/logs", "/minecraft/dynmap"]

EXPOSE 25565 25575 8123

WORKDIR /minecraft
ENTRYPOINT ["/usr/bin/entrypoint"]
CMD ["/bin/s6-svscan", "/etc/s6"]

ENV MINECRAFT_VERSION 1.13.2
ENV FORGE_VERSION 25.0.108
ENV FORGE_JAR forge-${MINECRAFT_VERSION}-${FORGE_VERSION}.jar
ENV FORGE_URL http://files.minecraftforge.net/maven/net/minecraftforge/forge/${MINECRAFT_VERSION}-${FORGE_VERSION}/forge-${MINECRAFT_VERSION}-${FORGE_VERSION}-installer.jar

RUN curl --create-dirs -sLo /minecraft/forge-${MINECRAFT_VERSION}-${FORGE_VERSION}-installer.jar ${FORGE_URL} && \
  cd /minecraft && \
  java -jar forge-${MINECRAFT_VERSION}-${FORGE_VERSION}-installer.jar --installServer && \
  rm -f /minecraft/forge-${MINECRAFT_VERSION}-${FORGE_VERSION}-installer.jar /minecraft/forge-${MINECRAFT_VERSION}-${FORGE_VERSION}-installer.jar.log

ADD rootfs /
ENV BUILD_CRAFT_JAR buildcraft-7.99.8.2.jar
RUN curl --create-dirs -sLo /minecraft/mods/${BUILD_CRAFT_JAR} https://mod-buildcraft.com/releases/BuildCraft/7.99.8.2/${BUILD_CRAFT_JAR}

ARG VERSION
ARG BUILD_DATE
ARG VCS_REF

LABEL org.label-schema.version=$VERSION
LABEL org.label-schema.build-date=$BUILD_DATE
LABEL org.label-schema.vcs-ref=$VCS_REF
LABEL org.label-schema.vcs-url="https://github.com/dockhippie/minecraft-forge.git"
LABEL org.label-schema.name="Minecraft Forge"
LABEL org.label-schema.vendor="Thomas Boerger"
LABEL org.label-schema.schema-version="1.0"
