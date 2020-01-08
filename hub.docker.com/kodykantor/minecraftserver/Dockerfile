FROM ubuntu:14.04
MAINTAINER Kody Kantor <Kody.Kantor@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update -y
# install default java, and supervisor
RUN apt-get install -y default-jre supervisor

# add the minecraft jar
ADD minecraft_server.1.7.10.jar /minecraft/minecraft-server.jar

ADD supervisord.conf /etc/supervisor/conf.d/supervisord.conf

EXPOSE 25565

CMD ["supervisord"]
