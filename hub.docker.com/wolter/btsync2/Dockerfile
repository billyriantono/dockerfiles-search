FROM debian:jessie

RUN adduser --uid 9991 --disabled-password --home=/btsync --gecos "" btsync

WORKDIR /btsync

RUN apt-get update -y && apt-get install -y wget && \
wget -O - http://download-cdn.getsyncapp.com/stable/linux-x64/BitTorrent-Sync_x64.tar.gz | tar xvfz - && \
rm -rf /var/lib/apt/lists/* && \
apt-get clean 

ADD btsync.conf /etc/
VOLUME /btsync/share /btsync/.sync
EXPOSE 8888
USER btsync
ENTRYPOINT /btsync/btsync --config /etc/btsync.conf --nodaemon
