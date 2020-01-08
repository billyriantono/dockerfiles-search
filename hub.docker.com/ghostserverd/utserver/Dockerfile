FROM lsiobase/xenial

RUN mkdir /utorrent && \
    curl -o utserver.tar.gz "http://download.ap.bittorrent.com/track/beta/endpoint/utserver/os/linux-x64-ubuntu-13-04" && \
    tar xvf utserver.tar.gz -C /utorrent/ && \
    apt-get update && \
    apt-get install -y libssl1.0.0 libssl-dev && \
    mv /utorrent/utorrent-server-alpha-v3_3/utserver /utorrent/utserver && \
    mv /utorrent/utorrent-server-alpha-v3_3/webui.zip /utorrent/webui.zip && \
    touch /utorrent/utserver.log && \
    mkdir -p /utorrent/settings && \
    mkdir -p /utorrent/data && \
    mkdir -p /config && \
    mkdir -p /downloads

COPY root/ /
COPY utserver.conf /config/utserver.conf

EXPOSE 6767 6881

VOLUME /config /downloads

