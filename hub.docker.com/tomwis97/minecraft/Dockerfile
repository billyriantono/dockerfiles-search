FROM tomwis97/minecraft:spigot
# Importing world
COPY world.tar.gz /opt/mc/world/world.tar.gz
RUN cd /opt/mc/world && \
    tar xvf world.tar.gz && \
    rm -f world.tar.gz
#COPY Projekt-Spawn.jar /opt/mc/plugins/ProjectSpawn.jar
COPY EssentialsX-2.0.1.jar /opt/mc/plugins/EssentialsX-2.0.1.jar
COPY ops.json /opt/mc/ops.json
COPY server.properties /opt/mc/server.properties
