# Bedrock Server
FROM ubuntu:latest

ENV APP_NAME="bedrockserver" IMG_NAME="bedrockserver" PKG_NAME="bedrockserver" EDGE=0 UNMASK=002

RUN mkdir /opt/bedrockserver
RUN apt-get update
RUN apt-get install -y unzip curl libcurl4 libssl1.0.0
RUN curl https://minecraft.azureedge.net/bin-linux/bedrock-server-1.11.4.2.zip --output bedrockserver.zip
RUN unzip bedrockserver.zip -d /opt/bedrockserver
RUN rm bedrockserver.zip

COPY server.properties /opt/bedrockserver/server.properties

VOLUME [ "/opt/bedrockserver" ]
EXPOSE 19132/udp
EXPOSE 19132/tcp

WORKDIR /opt/bedrockserver
ENV LD_LIBRARY_PATH /opt/bedrockserver
CMD cd /opt/bedrockserver && /opt/bedrockserver/bedrock_server
