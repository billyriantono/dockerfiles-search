FROM ubuntu:16.04

RUN apt-get -y update
RUN apt-get -y upgrade
RUN apt-get -y install default-jdk
RUN apt-get -y install wget

# Download Minecraft Server 1.9.4
RUN wget -O /minecraft_server.1.9.4.jar https://s3.amazonaws.com/Minecraft.Download/versions/1.9.4/minecraft_server.1.9.4.jar

# Sets working directory for the CMD instruction (also works for RUN, ENTRYPOINT commands)
WORKDIR /minecraft

# Accept Minecraft EULA,
RUN echo "eula=true" > /minecraft/eula.txt

# Expose the container's network port: 25565 during runtime.
EXPOSE 25565

# Start Minecraft server
CMD java -d64 -Xms768M -Xmx768M -jar /minecraft_server.1.9.4.jar nogui