# -----------------------------------------------------------------------------
# docker-minecraft
#
# Builds a basic docker image that can run a Minecraft server
# (http://minecraft.net/).
# -----------------------------------------------------------------------------

FROM openjdk:8u171-jre-stretch

LABEL maintainer "N00 Docker Team"

ENV DEBIAN_FRONTEND noninteractive

ENV VANILLA_VERSION=1.12.2


RUN apt-get --yes update; apt-get --yes upgrade
RUN apt-get --yes install curl ; apt-get clean

ADD ./scripts/start /start

RUN chmod +x /start

EXPOSE 25565

VOLUME ["/data"]

CMD ["/start"]