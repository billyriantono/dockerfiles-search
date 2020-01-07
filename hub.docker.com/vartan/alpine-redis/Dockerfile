FROM alpine:3.2

# add our user and group first to make sure their IDs get assigned consistently, regardless of whatever dependencies get added
RUN addgroup -S redis && adduser -S -G redis redis

# grab gosu for easy step-down from root
RUN apk add --update ca-certificates curl gnupg && \
    gpg --keyserver pool.sks-keyservers.net --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4 && \
    ARCH=`uname -m`; if [ $ARCH == "x86_64" ]; then export ARCH="amd64"; else export ARCH="i386"; fi && \
    curl -o /usr/local/bin/gosu -SL "https://github.com/tianon/gosu/releases/download/1.6/gosu-$ARCH" && \
    curl -o /usr/local/bin/gosu.asc -SL "https://github.com/tianon/gosu/releases/download/1.6/gosu-$ARCH.asc" && \
    gpg --verify /usr/local/bin/gosu.asc && \
	rm /usr/local/bin/gosu.asc && \
	chmod +x /usr/local/bin/gosu && \
    apk del ca-certificates curl gnupg && \
    rm -rf /var/cache/apk/*

ENV REDIS_VERSION 3.0.5
ENV REDIS_DOWNLOAD_URL http://download.redis.io/releases/redis-3.0.5.tar.gz
ENV REDIS_DOWNLOAD_SHA1 ad3ee178c42bfcfd310c72bbddffbbe35db9b4a6

# for redis-sentinel see: http://redis.io/topics/sentinel
RUN apk add --update ca-certificates curl gcc libc-dev make tar linux-headers && \
    mkdir -p /usr/src/redis && \
    curl -sSL "$REDIS_DOWNLOAD_URL" -o redis.tar.gz && \
    echo "$REDIS_DOWNLOAD_SHA1 *redis.tar.gz" | sha1sum -c - && \
    tar -xzf redis.tar.gz -C /usr/src/redis --strip-components=1 && \
    rm redis.tar.gz && \
    make -C /usr/src/redis MALLOC=libc && \
    make -C /usr/src/redis install && \
    rm -r /usr/src/redis && \
    apk del ca-certificates curl gcc libc-dev make tar linux-headers && \
    rm -rf /var/cache/apk/*

RUN mkdir /data && chown redis:redis /data
VOLUME /data
WORKDIR /data

COPY docker-entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]

EXPOSE 6379
CMD [ "redis-server" ]
