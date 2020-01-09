FROM ubuntu
MAINTAINER bn0ir <gblacknoir@gmail.com>

RUN apt-get update \
	&& apt-get install -y \
	    wget \
	&& mkdir -p /usr/local/src \
	&& mkdir -p /data/ \
	&& cd /usr/local/src \
	&& wget https://github.com/syncthing/discosrv/releases/download/v0.12.2/discosrv-linux-amd64.tar.gz \
	&& tar -xzf discosrv-linux-amd64.tar.gz \
	&& mkdir -p /usr/local/syncthing \
	&& cp discosrv-linux-amd64/discosrv /usr/local/syncthing/discosrv \
	&& rm -rf /usr/local/src/* /var/lib/apt/lists/* /tmp/* /var/tmp/*

ADD ./run_syncthing.sh /run_syncthing.sh

ENTRYPOINT ["bash"]

EXPOSE 8443

CMD ["/run_syncthing.sh"]
