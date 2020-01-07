FROM ubuntu:16.04

RUN apt-get update \
&& apt-get install -y apt-utils curl tzdata python\
&& curl -L https://yt-dl.org/latest/youtube-dl -o /usr/bin/youtube-dl \
&& chmod 755 /usr/bin/youtube-dl \
&& mkdir /download

WORKDIR /download
CMD youtube-dl
