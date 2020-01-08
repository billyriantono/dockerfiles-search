FROM openjdk:8u212-jre-alpine3.9 as builder

RUN mkdir -p /opt/spigot/src
WORKDIR /opt/spigot/src

RUN apk update && \
	apk add wget && \
	apk add git && \
	wget https://hub.spigotmc.org/jenkins/job/BuildTools/lastSuccessfulBuild/artifact/target/BuildTools.jar && \
	java -jar ./BuildTools.jar



FROM openjdk:8u212-jre-alpine3.9

RUN mkdir -p /opt/spigot/data
WORKDIR /opt/spigot/data

COPY --from=builder /opt/spigot/src/spigot-*.jar /opt/spigot/server.jar

EXPOSE 25565 20 21

ENTRYPOINT ["java", "-Xms1G", "-Xmx1G", "-XX:+UseConcMarkSweepGC", "-Dcom.mojang.eula.agree=true", "-jar", "./../server.jar"]
