FROM debian:jessie
MAINTAINER verti <vertical0520@gmail.com>

ADD start.sh /start.sh
RUN apt-get update && apt-get install -y wget git bzip2 && apt-get clean all && chmod 755 /start.sh \
	&& cd / \
	&& wget http://dl.4players.de/ts/releases/3.0.12.3/teamspeak3-server_linux_amd64-3.0.12.3.tar.bz2 \
	&& tar -xjf teamspeak3-server_linux_amd64-3.0.12.3.tar.bz2

EXPOSE 9987
VOLUME ["/data"]
ENTRYPOINT ["/start.sh"]

