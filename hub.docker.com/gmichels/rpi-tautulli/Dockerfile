FROM schmich/armv7hf-alpine-qemu
LABEL maintainer "gustavomichels@icloud.com"

ARG VERSION=2.1.37

WORKDIR /opt/Tautulli

RUN ["cross-build-start"]

RUN apk add --update python2 py-setuptools git wget && \
    rm -fr /var/cache/apk/* && \
    addgroup tautulli && adduser -D -H -h /opt/Tautulli -G tautulli -s /bin/ash tautulli && \ 
    wget -O tautulli.tar.gz https://github.com/Tautulli/Tautulli/archive/v${VERSION}.tar.gz && \
    tar xzfv tautulli.tar.gz --strip-components=1 && \
    chown -R tautulli:tautulli /opt/Tautulli && \
    rm tautulli.tar.gz

RUN ["cross-build-end"]

USER tautulli

VOLUME ["/config"]

ENTRYPOINT ["/usr/bin/python", "/opt/Tautulli/Tautulli.py", "--datadir", "/config"]
