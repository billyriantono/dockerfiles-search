FROM alpine:3.3
MAINTAINER Tomas Vercautter & Toon Lamberigts

ENV REDIS_VERSION=3.0.7
ENV REDIS_IMAGE=redis-$REDIS_VERSION
ENV REDIS_IMAGE_TAR=$REDIS_IMAGE.tar.gz
ENV REDIS_DOWNLOAD_URL=http://download.redis.io/releases/$REDIS_IMAGE_TAR

# Install redis
RUN apk --no-cache add --virtual .dependencies \
    make \
    gcc \
    wget \
    linux-headers \
    musl-dev \
    tcl \
    tar && \
    wget  "$REDIS_DOWNLOAD_URL" && \
    tar xzf $REDIS_IMAGE_TAR && \
    cd $REDIS_IMAGE && \
    make && \
    cp src/redis-server /usr/bin/ && \
    cp src/redis-cli /usr/bin/ && \
    rm -r /$REDIS_IMAGE && \
    rm -r /$REDIS_IMAGE_TAR && \
    apk del .dependencies && \
    rm -rf /var/cache/apk/* && \
    mkdir /data

VOLUME ["/data"]

CMD redis-server --dir /data --appendonly yes

# Expose the ports for redis
EXPOSE 6379