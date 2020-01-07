FROM storezhang/alpine

MAINTAINER storezhang "storezhang@gmail.com"
LABEL architecture="AMD64/x86_64" version="latest" build="2018-11-22"

EXPOSE 6379

ENV REDIS_VERSION 5.0.2
ENV REDIS_DOWNLOAD_URL http://download.redis.io/releases/redis-${REDIS_VERSION}.tar.gz

# 下载的Redis源代码SHA值，用来检验下载文件是不是可靠的
# ENV REDIS_DOWNLOAD_SHA 82a67c0eec97f9ad379384c30ec391b269e17a3e4596393c808f02db7595abcb

COPY docker-entrypoint.sh /usr/local/bin/
ADD redis.conf /

RUN set -ex \
    \
    && addgroup -S redis \
    && adduser -S -G redis redis \
    && apk add --no-cache --virtual .build-deps \
        'su-exec>=0.2' \
        coreutils \
        gcc \
        jemalloc-dev \
        linux-headers \
        make \
        musl-dev \
    && wget -O redis.tar.gz "${REDIS_DOWNLOAD_URL}" \
    # 检验下载文件是不是可靠的
    # && echo "${REDIS_DOWNLOAD_SHA} *redis.tar.gz" | sha256sum -c - \
    && mkdir -p /usr/src/redis \
    && tar -xzf redis.tar.gz -C /usr/src/redis --strip-components=1 \
    && rm redis.tar.gz \
    \
    && grep -q '^#define CONFIG_DEFAULT_PROTECTED_MODE 1$' /usr/src/redis/src/server.h \
    && sed -ri 's!^(#define CONFIG_DEFAULT_PROTECTED_MODE) 1$!\1 0!' /usr/src/redis/src/server.h \
    && grep -q '^#define CONFIG_DEFAULT_PROTECTED_MODE 0$' /usr/src/redis/src/server.h \
    \
    && make -C /usr/src/redis -j "$(nproc)" \
    && make -C /usr/src/redis install \
    \
    && rm -r /usr/src/redis \
    \
    && run_deps="$( \
        scanelf --needed --nobanner --format '%n#p' --recursive /usr/local \
            | tr ',' '\n' \
            | sort -u \
            | awk 'system("[ -e /usr/local/lib/" $1 " ]") == 0 { next } { print "so:" $1 }' \
    )" \
    && apk add --virtual .redis-rundeps ${run_deps} \
    && redis-server --version \
    && mkdir -p /redis/data \
    && chown -R redis:redis /redis \
    && apk del .build-deps \
        .redis-rundeps \
        coreutils \
        libattr \
        libacl \
        binutils \
        gmp \
        isl \
        libgomp \
        libatomic \
        pkgconf \
        libgcc \
        mpfr3 \
        mpc1 \
        libstdc++ \
        gcc \
        jemalloc \
        jemalloc-dev \
        linux-headers \
        make \
        musl-dev \
    && chmod +x /usr/local/bin/docker-entrypoint.sh \
    && ln -s /usr/local/bin/docker-entrypoint.sh / \
    && rm -rf /var/cache/apk/*

VOLUME /redis
WORKDIR /redis/data

ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["redis-server"]
