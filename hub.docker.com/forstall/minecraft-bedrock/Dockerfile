FROM ubuntu:latest

RUN apt-get update
RUN apt-get install -y unzip curl libcurl4 libssl1.0.0


# update this when the server version changes
RUN curl https://minecraft.azureedge.net/bin-linux/bedrock-server-1.11.4.2.zip --output bedrock-server.zip
# unzip it to the mount
RUN unzip bedrock-server.zip -d minecraft
# delete the file
RUN rm bedrock-server.zip

RUN mv /minecraft/server.properties /minecraft/config && \
    mv /minecraft/permissions.json /minecraft/config && \
    mv /minecraft/whitelist.json /minecraft/config && \
    ln -s /minecraft/config/server.properties /minecraft/server.properties && \
    ln -s /minecraft/config/permissions.json /minecraft/permissions.json && \
ln -s /minecraft/config/whitelist.json /minecraft/whitelist.json

# Set the working directory to the mount
WORKDIR /minecraft

ENV LD_LIBRARY_PATH=.
# CMD ./minecraft/bedrock_server
