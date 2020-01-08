FROM ubuntu:latest

ARG BEDROCK_VERSION=1.12.0.28

RUN apt-get update
RUN apt-get install -y unzip curl libcurl4 libssl1.0.0 net-tools
RUN curl https://minecraft.azureedge.net/bin-linux/bedrock-server-${BEDROCK_VERSION}.zip --output bedrock-server.zip
RUN unzip bedrock-server.zip -d bedrock-server
RUN rm bedrock-server.zip

EXPOSE 19132

WORKDIR /bedrock-server
ENV LD_LIBRARY_PATH=.
CMD ./bedrock_server
