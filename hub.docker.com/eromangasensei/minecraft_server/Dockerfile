FROM java
Run mkdir -p /data/minecraft_server && \
    wget https://launcher.mojang.com/v1/objects/3dc3d84a581f14691199cf6831b71ed1296a9fdf/server.jar -O /data/minecraft_server/server.jar && \
    echo "eula=true" > /data/minecraft_server/eula.txt
    CMD [ "sh", "-c", "cd /data/minecraft_server && java -jar server.jar"]
Expose 25565
VOLUME /data/minecraft_server
