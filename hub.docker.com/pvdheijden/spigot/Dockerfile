FROM openjdk:11-jdk-slim

ARG MINECRAFT_REV

LABEL minecraft.version=$MINECRAFT_REV
LABEL buildtools.version="latest"

ADD https://hub.spigotmc.org/jenkins/job/BuildTools/lastSuccessfulBuild/artifact/target/BuildTools.jar /tmp/spigot/BuildTools.jar

RUN apt-get update && apt-get install -y git && \
    cd /tmp/spigot && java -Xms1G -jar BuildTools.jar --rev $MINECRAFT_REV && \
    mkdir -p /opt/minecraft/data && \
    mv /tmp/spigot/spigot*.jar /opt/minecraft && \
    rm -r /tmp/spigot && \
    ln -s /opt/minecraft/spigot*.jar /opt/minecraft/spigot.jar

RUN adduser --system --group minecraft && \
    chown -R minecraft:minecraft /opt/minecraft
USER minecraft

VOLUME /opt/minecraft/data
EXPOSE 25565
EXPOSE 25575

WORKDIR /opt/minecraft/data
COPY --chown=minecraft:minecraft eula.txt ./

ENV JAVA_OPTS -Xms1G -Xmx4G

ENTRYPOINT exec java \
    -XX:+UnlockExperimentalVMOptions \
    $JAVA_OPTS -jar /opt/minecraft/spigot.jar nogui --noconsole
