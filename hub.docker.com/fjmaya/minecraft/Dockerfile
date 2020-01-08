# Minecraft Server Dockerfile


# FROM library/java:latest
FROM library/java:latest

MAINTAINER Javier Sanchez

ARG MC_VERSION=1.8.8-11.15.0.1655

RUN mkdir /minecraft

# Download Minecraft Server components
#RUN wget -q https://s3.amazonaws.com/Minecraft.Download/versions/$MC_VERSION/minecraft_server.$MC_VERSION.jar -O /minecraft/minecraft_server.jar
RUN wget -q http://files.minecraftforge.net/maven/net/minecraftforge/forge/$MC_VERSION/forge-$MC_VERSION-installer.jar -O /minecraft/forge-$MC_VERSION-installer.jar ;\
cd /minecraft ;\
java -jar forge-$MC_VERSION-installer.jar --installServer ;\
rm /minecraft/forge-$MC_VERSION-installer.jar ;\
mv /minecraft/forge-$MC_VERSION-universal.jar /minecraft/forge-universal.jar

# Sets working directory for the CMD instruction (also works for RUN, ENTRYPOINT commands)
# Create mount point, and mark it as holding externally mounted volume
WORKDIR /data
VOLUME /data

# Expose the container's network port: 25565 during runtime.
EXPOSE 25565

#Automatically accept Minecraft EULA, and start Minecraft server
CMD echo eula=true > /data/eula.txt && java -jar /minecraft/forge-universal.jar
