FROM ich777/novnc-baseimage

LABEL maintainer="admin@minenet.at"

RUN apt-get update && \
	apt-get -y install --no-install-recommends bzip2 && \
	rm -rf /var/lib/apt/lists/* && \
	sed -i '/    document.title =/c\    document.title = "Firefox - noVNC";' /usr/share/novnc/app/ui.js && \
	rm /usr/share/novnc/app/images/icons/*

ENV DATA_DIR=/firefox
ENV CUSTOM_RES_W=1280
ENV CUSTOM_RES_H=1024
ENV FIREFOX_V="latest"
ENV FIREFOX_LANG="en-US"
ENV FORCE_UPDATE=""
ENV UMASK=000
ENV UID=99
ENV GID=100

RUN mkdir $DATA_DIR && \
	useradd -d $DATA_DIR -s /bin/bash --uid $UID --gid $GID firefox && \
	chown -R firefox $DATA_DIR && \
	ulimit -n 2048

ADD /scripts/ /opt/scripts/
RUN chmod -R 770 /opt/scripts/ && \
	chown -R firefox /opt/scripts

USER firefox

#Server Start
ENTRYPOINT ["/opt/scripts/start-server.sh"]