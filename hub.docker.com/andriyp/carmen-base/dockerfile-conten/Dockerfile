FROM alpine:3.8

ARG DUMB_INIT_VERSION=1.2.2

ENV \
    TERM=xterm-color           \
    TIME_ZONE=Europe/Berlin  \
    MYUSER=app                 \
    MYUID=1001                 \
    DOCKER_GID=999

RUN \
    apk update && apk upgrade && \
    apk add --no-cache su-exec tzdata curl openssl && \
    mkdir -p /home/$MYUSER && \
    adduser -s /bin/sh -D -u $MYUID $MYUSER && chown -R $MYUSER:$MYUSER /home/$MYUSER && \
    delgroup ping && addgroup -g 998 ping && \
    addgroup -g ${DOCKER_GID} docker && addgroup ${MYUSER} docker && \
    mkdir -p /srv && chown -R $MYUSER:$MYUSER /srv && \
    cp /usr/share/zoneinfo/${TIME_ZONE} /etc/localtime && \
    echo "${TIME_ZONE}" > /etc/timezone && date && \
    wget -q https://github.com/Yelp/dumb-init/releases/download/v${DUMB_INIT_VERSION}/dumb-init_${DUMB_INIT_VERSION}_amd64 -O /usr/bin/dumb-init && \
    chmod +x /usr/bin/dumb-init && \
    rm -rf /var/cache/apk/*

ENTRYPOINT ["/usr/bin/dumb-init", "--"]
