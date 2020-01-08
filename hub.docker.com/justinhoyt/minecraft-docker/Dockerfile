# docker run -d -p 25565:25565 -t justinhoyt/minecraft
FROM library/java:latest
RUN mkdir /mc
WORKDIR /mc
ADD \
  banned-ips.json \
  banned-players.json \
  minecraft_server.1.12.1.jar \
  ops.json \
  server.properties \
  whitelist.json \
  eula.txt \
  ./
EXPOSE 25565
CMD ["java", "-Xmx1024M","-Xms1024M","-jar","minecraft_server.1.12.1.jar","nogui"]