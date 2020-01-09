FROM debian:latest
MAINTAINER adrian@silaghi.me

USER root:root
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && \
	apt-get install	-y apt-utils && \
	apt-get upgrade -y && \
	apt-get install -y wget sudo gnupg2 procps && \
	apt-get install -y openjdk-8-jre-headless jsvc && \
	apt-get install -y mongodb-server mongodb-clients lsb-release

RUN wget -O unifi-video.key http://www.ubnt.com/downloads/unifi-video/apt-3.x/unifi-video.gpg.key && \
	apt-key add unifi-video.key && rm -f unifi-video.key && \
	sh -c "echo \"deb [arch=amd64] http://www.ubnt.com/downloads/unifi-video/apt-3.x wheezy ubiquiti\" > /etc/apt/sources.list.d/unifi-video.list"

RUN apt-get update && \
	apt-get install unifi-video

RUN echo '#!/bin/bash\n\
chown unifi-video:unifi-video /var/lib/unifi-video\n\
chmod 755 /var/lib/unifi-video\n\
apt-get update\n\
apt-get install -y --only-upgrade unifi-video\n\
sed -i /ulimit/d /usr/sbin/unifi-video\n\
/usr/sbin/unifi-video --debug -D start' > /run.sh && chmod +x /run.sh

VOLUME /var/lib/unifi-video/

# RTMP, RTMPS & RTSP via the controller
EXPOSE 1935/tcp 7444/tcp 7447/tcp 6666/tcp 7442/tcp 7004/udp 7080/tcp 7443/tcp 7445/tcp 7446/tcp

ENTRYPOINT ["/run.sh"]


