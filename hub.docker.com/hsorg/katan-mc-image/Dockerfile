# Katan Minecraft Dockerfile
# Use official Debian Docker image
FROM debian:stretch

MAINTAINER Natan V <itroken99@gmail.com>

# Minecraft server version to download
ENV MINECRAFT_VERSION 1.8.8-R0.1

# Minecraft server dist? craftbukkit, spigot or vanilla
ENV MINECRAFT_DIST spigot

RUN apt update; \
    apt install -y default-jre ca-certificates-java wget; \
    wget -q https://cdn.getbukkit.org/${MINECRAFT_DIST}/${MINECRAFT_DIST}-${MINECRAFT_VERSION}-SNAPSHOT-latest.jar -O /${MINECRAFT_DIST}-${MINECRAFT_VERSION}-SNAPSHOT-latest.jar

# Set server working directory
WORKDIR /server
VOLUME /server

# Accept EULA and start the server
CMD echo eula=true > /server/eula.txt && java -jar /${MINECRAFT_DIST}-${MINECRAFT_VERSION}-SNAPSHOT-latest.jar