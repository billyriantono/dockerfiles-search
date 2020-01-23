# Dockerfile for gitkraken to install
FROM ubuntu:16.04

WORKDIR /home

RUN apt-get update && \
		apt-get install -y wget gconf2 gconf-service libgtk2.0-0 libnotify4 libxtst6 libnss3 python gvfs-bin xdg-utils firefox libgnome-keyring0 curl libcurl3 libxss1

RUN wget --quiet "https://release.gitkraken.com/linux/gitkraken-amd64.deb" -O gitkraken-amd64.deb && \
  	dpkg -i gitkraken-amd64.deb; apt-get install -f -y  && \
		rm -rf /var/lib/apt/lists/* && \
  	rm gitkraken-amd64.deb

RUN groupadd -r developer -g 1000 && \
    useradd -u 1000 -r -g developer -d /developer -s /bin/bash -c "Software Developer" developer && \
    mkdir /developer && \
    mkdir /developer/.gitkraken && \
    chown -R developer:developer /developer

USER developer

ENV DISPLAY 192.168.1.8:0

VOLUME ["/developer"]

CMD ["/usr/bin/gitkraken"]