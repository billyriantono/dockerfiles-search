FROM        ubuntu:18.04 AS base

WORKDIR     /tmp/workdir

RUN     apt-get -yqq update && \
        apt-get install -yq --no-install-recommends ca-certificates expat libgomp1 && \
        apt-get autoremove -y && \
        apt-get clean -y
RUN 	apt-get install -y python-pip eyed3 ffmpeg wget curl && \
        apt-get autoremove -y && \
        apt-get clean -y
RUN		pip install youtube-dl
COPY    mkpodcast  /usr/local/bin
RUN		chmod +x /usr/local/bin/mkpodcast
WORKDIR     /data
