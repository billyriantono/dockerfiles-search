# Minecraft Server Image
# From Java v8
FROM openjdk:8-jre-alpine

LABEL maintainer="Reed Bender <reedbndr@gmail.com>"

# Specify Minecraft Version and server jar file
ENV MINECRAFT_VER=1.14.4
ENV MINECRAFT_JAR="https://launcher.mojang.com/v1/objects/3dc3d84a581f14691199cf6831b71ed1296a9fdf/server.jar"

# Download dependencies
RUN apk add --no-cache -U \
  bash \
  curl \
  wget \
  ca-certificates

RUN apk update

# Download jar file
RUN mkdir -p /opt/minecraft \
  && cd /opt/minecraft \
  && wget -q $MINECRAFT_JAR -O minecraft_server.jar \
  && java -Xms1024M -Xmx1536M -jar minecraft_server.jar \
  && echo 'eula=true' > eula.txt 

WORKDIR /data
VOLUME /data

# Expose the port to Minecraft
EXPOSE 25565




