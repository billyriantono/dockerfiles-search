FROM ubuntu

MAINTAINER kingedgar

RUN apt-get update && apt-get -y install wget screen iproute2 iputils-ping net-tools

ENV DATA_DIR="/serverdata"
ENV SERVER_DIR="${DATA_DIR}/serverfiles"
ENV RUNTIME_NAME="template"
ENV JAR_NAME="template"
ENV GAME_PARAMS=""
ENV GAME_PORT=25565
ENV XMX_SIZE=1024
ENV XMS_SIZE=1024
ENV ACCEPT_EULA="false"
ENV UID=1000
ENV GID=1002

RUN mkdir $DATA_DIR && mkdir $SERVER_DIR
RUN groupadd --gid $GID minecraft && useradd -d $DATA_DIR -s /bin/bash --uid $UID --gid $GID minecraft
RUN chown -R $UID:$GID $DATA_DIR
RUN chmod -R 770 $DATA_DIR

RUN ulimit -n 2048

ADD /scripts/ /opt/scripts/
RUN chmod -R 770 /opt/scripts/
RUN chown -R minecraft:minecraft /opt/scripts

USER minecraft

#Server Start
ENTRYPOINT ["/opt/scripts/start-server.sh"]
