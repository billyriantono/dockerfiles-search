FROM alpine:3.6
MAINTAINER Bertus Steenberg

ENV RPCPORT 9091
ENV PEERPORT 45555
ENV USERNAME username
ENV PASSWORD=

COPY config/settings.json /config/settings.json

# install packages
RUN \
    apk update && \
    apk add --no-cache \
        curl \
        jq \
        openssl \
        p7zip \
        tar \
        transmission-cli \
        transmission-daemon \
        unrar \
        unzip

COPY entrypoint.sh /usr/bin/entrypoint.sh
RUN chmod u+x  /usr/bin/entrypoint.sh

VOLUME ["/downloads", "/incomplete", "/watch", "/config"]

EXPOSE $RPCPORT $PEERPORT $PEERPORT/UDP

ENTRYPOINT ["/usr/bin/entrypoint.sh"]

CMD /usr/bin/transmission-daemon \
    --foreground \
    --config-dir /config \ 
    --log-info \
    --peerport ${PEERPORT} \
    --username ${USERNAME} \
    --password ${PASSWORD} \
    --auth \
    --watch-dir /watch \
    --download-dir /downloads \
    --incomplete-dir /incomplete