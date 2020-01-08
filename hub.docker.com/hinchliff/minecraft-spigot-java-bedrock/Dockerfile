FROM gradle:jdk8 as builder

# Build 'mcpenew' branch of ProtocolSupport
RUN cd /home/gradle && \
    git clone --single-branch --branch mcpenew https://github.com/ProtocolSupport/ProtocolSupport.git && \
    cd ProtocolSupport && \
    ./gradlew --no-daemon jar

FROM openjdk:8-jre-slim

# Download last version of spigot
ENV SPIGOT_VER 1.14.3
RUN apt-get update \
	&& apt-get -y upgrade \
	&& apt-get -y install git curl \
        && mkdir -p /spigot \
	&& cd /spigot \
        && curl -Ss -o /spigot/BuildTools.jar https://hub.spigotmc.org/jenkins/job/BuildTools/lastSuccessfulBuild/artifact/target/BuildTools.jar \
	&& java -jar BuildTools.jar --rev $SPIGOT_VER \
        && rm -rf /spigot/BuildData /spigot/BuildTools.jar /spigot/Bukkit /spigot/CraftBukkit /spigot/Spigot /spigot/apache-maven-* /spigot/work  /root/.m2 \
        && apt-get -y autoremove --purge \
        && rm -rf /var/lib/apt/lists/*

EXPOSE 25565 25565/udp

# /data contains static files and database
VOLUME ["/data"]

WORKDIR /data

# add ProtocolSupport plugin
RUN mkdir -p /data/plugins
COPY --from=builder /home/gradle/ProtocolSupport/target/ProtocolSupport.jar /data/plugins/ProtocolSupport.jar

# start the server
CMD java -Xms512M -Xmx1008M -Dcom.mojang.eula.agree=true -Dfile.encoding=UTF-8 -jar /spigot/spigot-${SPIGOT_VER}.jar nogui
