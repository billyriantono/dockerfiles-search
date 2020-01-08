# Java Version
ARG JAVA_VERSION=11

FROM openjdk:${JAVA_VERSION} AS build

LABEL maintainer="DarrylSSY <ssy.darryl@gmail.com>"

# PaperSpigot
ARG PAPERSPIGOT_CI_JOB=Paper-1.14
ARG PAPERSPIGOT_CI_BUILDNUMBER=lastStableBuild
ARG ARTIFACT_NAME=paperclip.jar
ARG PAPERSPIGOT_CI_URL=https://papermc.io/ci/job/${PAPERSPIGOT_CI_JOB}/${PAPERSPIGOT_CI_BUILDNUMBER}/artifact/${ARTIFACT_NAME}

# Server Files
ARG USERNAME=astenity-mc
ENV SERVER_PATH=/opt/minecraft
WORKDIR ${SERVER_PATH}

# DOWNLOAD FILES
ADD ${PAPERSPIGOT_CI_URL} paperclip.jar

# Manage user
RUN useradd -ms /bin/bash ${USERNAME} && \
    chown ${USERNAME} ${SERVER_PATH} -R

USER ${USERNAME}

# RUN SERVER
RUN java -jar ${SERVER_PATH}/paperclip.jar; exit 0

# COPY BUILT JAR
RUN mv ${SERVER_PATH}/cache/patched*.jar ${SERVER_PATH}/paperspigot.jar

# Running environment
FROM openjdk:${JAVA_VERSION} AS runtime

# Environment
ENV MINECRAFT_PATH=/opt/minecraft
ENV SERVER_PATH=${MINECRAFT_PATH}/server
ENV DATA_PATH=${MINECRAFT_PATH}/data
ENV LOGS_PATH=${MINECRAFT_PATH}/logs
ENV CONFIG_PATH=${MINECRAFT_PATH}/config
ENV WORLDS_PATH=${MINECRAFT_PATH}/worlds
ENV PLUGINS_PATH=${MINECRAFT_PATH}/plugins
ENV PROPERTIES_LOCATION=${CONFIG_PATH}/server.properties
ENV JAVA_HEAP_SIZE=4G
ENV JAVA_ARGS="-Xmx${JAVA_HEAP_SIZE} -Xms${JAVA_HEAP_SIZE} -XX:+UseConcMarkSweepGC -server -Dcom.mojang.eula.agree=true"
ENV SPIGOT_ARGS="--nojline --bukkit-settings ${CONFIG_PATH}/bukkit.yml --plugins ${PLUGINS_PATH} --world-dir ${WORLDS_PATH} --spigot-settings ${CONFIG_PATH}/spigot.yml --commands-settings ${CONFIG_PATH}/commands.yml --config ${PROPERTIES_LOCATION}"
ENV PAPERSPIGOT_ARGS="--paper-settings ${CONFIG_PATH}/paper.yml"

# Install mcstatus
ADD https://bootstrap.pypa.io/get-pip.py get-pip.py
RUN python get-pip.py
RUN pip install mcstatus

# Check status
HEALTHCHECK --interval=10s --timeout=5s \
    CMD mcstatus localhost:$( cat $PROPERTIES_LOCATION | grep "server-port" | cut -d'=' -f2 ) ping

# Setup server files
WORKDIR ${MINECRAFT_PATH}
COPY --from=build /opt/minecraft/paperspigot.jar ${SERVER_PATH}/

# Obtain scripts
ADD scripts/start.sh start.sh

# User
RUN addgroup minecraft && \
    useradd -ms /bin/bash minecraft -g minecraft -d ${MINECRAFT_PATH} && \
    mkdir ${LOGS_PATH} ${DATA_PATH} ${WORLDS_PATH} ${PLUGINS_PATH} ${CONFIG_PATH} && \
    chown -R minecraft:minecraft ${MINECRAFT_PATH}
USER minecraft

# Volumes
VOLUME "${CONFIG_PATH}"
VOLUME "${WORLDS_PATH}"
VOLUME "${PLUGINS_PATH}"
VOLUME "${DATA_PATH}"
VOLUME "${LOGS_PATH}"

# Ports
EXPOSE 25565

# Run start script
ENTRYPOINT bash start.sh