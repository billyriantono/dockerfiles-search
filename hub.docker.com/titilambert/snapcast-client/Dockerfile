FROM debian:unstable-20190326-slim

ENV SNAP_VERSION 0.15.0
RUN apt-get update && \
	apt-get install -y wget && \
	wget https://github.com/badaix/snapcast/releases/download/v${SNAP_VERSION}/snapclient_${SNAP_VERSION}_armhf.deb && \
    ( dpkg -i snapclient_*_amd64.deb || true ) && \
	apt-get install -f -y && \
	apt-get purge wget -y && \
    rm -f snapclient_*_amd64.deb

ENTRYPOINT /usr/bin/snapclient
