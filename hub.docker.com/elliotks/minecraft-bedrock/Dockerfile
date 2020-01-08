FROM ubuntu:latest
LABEL Name=elliotks/minecraft-bedrock Version=1.14.1.4
# set minecraft bedrock server version to download.
ENV MCBR_VER="1.14.1.4"

# config server
ENV LD_LIBRARY_PATH . 
ENV SERVER_HOME="/minecraft-bedrock" \
  SERVER_PATH="/minecraft-bedrock/server" \
  SCRIPT_PATH="/minecraft-bedrock/script" \
  DEFAULT_CONFIG_PATH="/minecraft-bedrock/default-config" \
  DATA_PATH="/minecraft-bedrock/data"

RUN apt-get update && \
 apt-get -y install curl libcurl4 unzip libssl1.0.0 && \
 apt-get -y autoremove && \
 apt-get clean

RUN addgroup --gid 1000 mcbedrock
RUN adduser --disabled-password --gecos "" --force-badname --gid 1000 --uid 1000 mcbedrock

# Download version specified in ENV MCBR_VER, unzip to SERVER_PATH, Move Configs to DEFAULT_CONFIG_PATH
RUN mkdir -p $DATA_PATH
RUN mkdir -p $SERVER_PATH
RUN curl https://minecraft.azureedge.net/bin-linux/bedrock-server-${MCBR_VER}.zip --output /tmp/bedrock.zip
RUN unzip /tmp/bedrock.zip -d $SERVER_PATH
RUN mkdir -p $DEFAULT_CONFIG_PATH
RUN mv $SERVER_PATH/permissions.json $DEFAULT_CONFIG_PATH && mv $SERVER_PATH/server.properties $DEFAULT_CONFIG_PATH && mv $SERVER_PATH/whitelist.json $DEFAULT_CONFIG_PATH
RUN rm /tmp/bedrock.zip
RUN chown -R mcbedrock:mcbedrock /minecraft-bedrock

# copy scripts over.
COPY ./script $SCRIPT_PATH
RUN chmod +x $SCRIPT_PATH/start.sh

USER mcbedrock

WORKDIR ${SERVER_PATH}
EXPOSE 19132/udp 
EXPOSE 19133/udp

VOLUME ["/minecraft-bedrock/data"]

# RUN 
CMD ["/minecraft-bedrock/script/start.sh"]
