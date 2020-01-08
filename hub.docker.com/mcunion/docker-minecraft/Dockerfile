FROM openjdk:7-jre-alpine

ENV JAVA_HOME=/usr/lib/jvm/default-jvm \
    JVM_OPTS=-Xmx1024M \
    SERVER_JAR=minecraft_server.jar \
    LANG=C.UTF-8

RUN ln -sf "${JAVA_HOME}/bin/"* "/usr/bin/" && \
    adduser -SD -u 1000 minecraft 

USER minecraft

EXPOSE 25565

WORKDIR /minecraft/server

COPY start.sh /start
CMD ["/bin/sh","/start"]
