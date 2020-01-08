FROM linuxserver/qbittorrent

RUN apt-get update \
 && apt-get install -y rsync \
 && mkdir /torrents \
 && mkdir /scripts \
 && chown abc:abc /torrents \
 && chown abc:abc /scripts \
 && apt-get clean \
 && rm -rf \
    /tmp/* \
    /var/lib/apt/lists/* \
    /var/tmp/*
    
EXPOSE 6881 6881/udp 8080

VOLUME /config /downloads /torrents /scripts
