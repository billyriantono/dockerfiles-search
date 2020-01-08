FROM openjdk:8-jre
LABEL maintainer "yuki0308"

EXPOSE 25565
VOLUME ["/data"]
WORKDIR /data

CMD java -DIReallyKnowWhatIAmDoingISwear -Dcom.mojang.eula.agree=true -Xmx${MAX_MEMORY}M -jar spigot.jar
