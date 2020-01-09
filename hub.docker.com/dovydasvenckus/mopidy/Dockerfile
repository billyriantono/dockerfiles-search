FROM debian:buster
MAINTAINER dovydas.venckus@live.com

EXPOSE 6600 6800
COPY entrypoint.sh /
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y wget gnupg && \
    wget -q -O - https://apt.mopidy.com/mopidy.gpg | apt-key add - && \
    wget -q -O /etc/apt/sources.list.d/mopidy.list https://apt.mopidy.com/buster.list && \
    apt-get update && \
    apt-get install -y mopidy mopidy-local-sqlite mopidy-scrobbler python-pip && \
    pip install Mopidy-Iris && \
    pip install Mopidy-MusicBox-Webclient

ENTRYPOINT ["/bin/sh", "entrypoint.sh"]
