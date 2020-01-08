FROM java:8
RUN wget -q https://s3.amazonaws.com/Minecraft.Download/versions/1.9/minecraft_server.1.9.jar
WORKDIR /data
VOLUME /data
EXPOSE 25565
CMD echo eula=true > /data/eula.txt && java -jar /minecraft_server.1.9.jar
