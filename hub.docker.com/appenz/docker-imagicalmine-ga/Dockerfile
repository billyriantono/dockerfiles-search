FROM ubuntu:14.04

MAINTAINER appenz https://github.com/appenz

RUN apt-get update -y
RUN apt-get upgrade -y
RUN apt-get install -y \
        wget \
	curl \
        perl gcc g++ make automake libtool autoconf m4 \
        gcc-multilib \
	libltdl-dev \
	unzip

RUN adduser --gecos 'PocketMine-MP' --disabled-password --home /pocketmine pocketmine

WORKDIR /pocketmine
RUN mkdir /pocketmine/IM
RUN chown -R pocketmine:pocketmine /pocketmine

COPY assets/entrypoint.sh /pocketmine/entrypoint.sh

RUN chmod 755 /pocketmine/entrypoint.sh

USER pocketmine

RUN curl -sL http://get.imagicalmine.net > init.sh

EXPOSE 19132
EXPOSE 19132/udp

ENTRYPOINT ["./entrypoint.sh"]
