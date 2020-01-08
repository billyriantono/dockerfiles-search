FROM docku/jre7
MAINTAINER Jon Chen <bsd@voltaire.sh>

EXPOSE 25565

VOLUME ["/srv/minecraft/world"]

ADD https://s3.amazonaws.com/Minecraft.Download/versions/1.8/minecraft_server.1.8.jar /srv/minecraft/minecraft.jar
ADD start /srv/minecraft/start
ADD eula.txt /srv/minecraft/eula.txt

ADD run /service/minecraft/run
