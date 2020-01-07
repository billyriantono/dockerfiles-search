FROM ubuntu:latest
MAINTAINER kjbweb <mail@kjbweb.net>

RUN apt-get update && \
    apt-get install ffmpeg curl python locales locales-all -y && \
    curl -L https://yt-dl.org/downloads/latest/youtube-dl -o /usr/local/bin/youtube-dl && \
    chmod a+rx /usr/local/bin/youtube-dl

ENV LANG en_GB.UTF-8
ENV LANGUAGE en_GB:en
ENV LC_ALL en_GB.UTF-8

CMD [ "/usr/local/bin/youtube-dl" ]
