FROM ubuntu:latest

RUN apt-get update
RUN apt-get install -y unzip curl
RUN url=$(curl -s -L https://minecraft.net/en-us/download/server/bedrock/ | grep bin-linux | sed "s/.*href=['\"]\([^'\"]*\)['\"].*/\1/g"); curl $url --output bedrock.zip
RUN unzip bedrock.zip -d MinecraftBDE
RUN rm bedrock.zip

WORKDIR /MinecraftBDE
ENV LD_LIBRARY_PATH=.
CMD ./bedrock_server

EXPOSE 19132/udp
VOLUME /MinecraftBDE/worlds
