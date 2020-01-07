FROM ascdc/apache2-php56
MAINTAINER ASCDC <asdc.sinica@gmail.com>

ADD run.sh /script/run.sh

RUN DEBIAN_FRONTEND=noninteractive && \
	chmod +x /script/*.sh && \
	apt-get update && \
	apt-get -y dist-upgrade && \
	apt-get -y install cron curl wget && \
	locale-gen en_US.UTF-8 && \
	export LANG=en_US.UTF-8

WORKDIR /script
ENTRYPOINT ["/script/run.sh"]
