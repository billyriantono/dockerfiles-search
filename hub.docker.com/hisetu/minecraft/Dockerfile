FROM dockerfile/java:oracle-java8

RUN mkdir /app && \
	cd /app && \
	wget -O minecraft_server.jar -nv https://s3.amazonaws.com/Minecraft.Download/versions/1.8.1/minecraft_server.1.8.1.jar && \
	java -Xmx1024M -Xms1024M -jar minecraft_server.jar nogui

COPY start /app/start
COPY server.properties /app/server.properties

WORKDIR /app
CMD ["bash", "start"]

EXPOSE 25565
EXPOSE 25575