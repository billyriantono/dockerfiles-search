FROM webhippie/java:latest
MAINTAINER Thomas Boerger <thomas@webhippie.de>

VOLUME ["/minecraft/merge", "/minecraft/world", "/minecraft/logs"]

EXPOSE 25565 25575

WORKDIR /minecraft
ENTRYPOINT ["/usr/bin/entrypoint"]
CMD ["/bin/s6-svscan", "/etc/s6"]

ENV MINECRAFT_JAR server.jar
ENV MINECRAFT_URL https://launcher.mojang.com/v1/objects/4d1826eebac84847c71a77f9349cc22afd0cf0a1/${MINECRAFT_JAR}

RUN curl --create-dirs -sLo /minecraft/${MINECRAFT_JAR} ${MINECRAFT_URL}

ADD rootfs /

ARG VERSION
ARG BUILD_DATE
ARG VCS_REF

LABEL org.label-schema.version=$VERSION
LABEL org.label-schema.build-date=$BUILD_DATE
LABEL org.label-schema.vcs-ref=$VCS_REF
LABEL org.label-schema.vcs-url="https://github.com/Desnoo/minecraft-vanilla"
LABEL org.label-schema.name="Minecraft Vanilla"
LABEL org.label-schema.vendor="Desnoo based on Thomas Boerger"
LABEL org.label-schema.schema-version="1.0"
