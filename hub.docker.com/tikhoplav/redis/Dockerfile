FROM centos:centos7

RUN echo "Europe/Moscov" > /etc/timezone
RUN localedef -i ru_RU -f UTF-8 ru_RU.UTF-8

RUN groupadd -r redis --gid=1000; \
	useradd -r -g redis --uid=1000 redis;

ENV GOSU_VERSION 1.10
RUN set -x && \
    curl -Lo /usr/bin/gosu "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-amd64" && \
    curl -Lo /tmp/gosu.asc "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-amd64.asc" && \
    export GNUPGHOME="$(mktemp -d)" && \
    for server in $(shuf -e ha.pool.sks-keyservers.net \
                            hkp://p80.pool.sks-keyservers.net:80 \
                            keyserver.ubuntu.com \
                            hkp://keyserver.ubuntu.com:80 \
                            pgp.mit.edu) ; do \
        gpg --keyserver "$server" --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4 && break || : ; \
    done && \
    gpg --batch --verify /tmp/gosu.asc /usr/bin/gosu && \
    rm -r "$GNUPGHOME" /tmp/gosu.asc && \
    chmod +x /usr/bin/gosu && \
    # Allow user to become root
    #chmod u+s /usr/bin/gosu && \
    gosu nobody true

RUN yum update -y; yum clean all

ENV REDIS_VERSION 5.0.5
ENV REDIS_DOWNLOAD_URL http://download.redis.io/releases/redis-5.0.5.tar.gz
ENV REDIS_DOWNLOAD_SHA 2139009799d21d8ff94fc40b7f36ac46699b9e1254086299f8d3b223ca54a375

RUN yum install -y ca-certificates wget gcc libc6-dev make; \
    yum clean all; \
    wget -O redis.tar.gz "$REDIS_DOWNLOAD_URL"; \
    echo "$REDIS_DOWNLOAD_SHA *redis.tar.gz" | sha256sum -c -; \
    mkdir -p /usr/src/redis; \
    tar -xzf redis.tar.gz -C /usr/src/redis --strip-components=1; \
    rm redis.tar.gz; \
    grep -q '^#define CONFIG_DEFAULT_PROTECTED_MODE 1$' /usr/src/redis/src/server.h; \
    sed -ri 's!^(#define CONFIG_DEFAULT_PROTECTED_MODE) 1$!\1 0!' /usr/src/redis/src/server.h; \
    grep -q '^#define CONFIG_DEFAULT_PROTECTED_MODE 0$' /usr/src/redis/src/server.h; \
    make -C /usr/src/redis -j "$(nproc)"; \
    make -C /usr/src/redis install; \
    rm -r /usr/src/redis; \
    yum remove -y -y ca-certificates wget gcc libc6-dev make; \
    yum clean all;

RUN mkdir /data && chown redis:redis /data

VOLUME ["/data"]

WORKDIR /data

EXPOSE 6379

USER redis

CMD ["redis-server"]