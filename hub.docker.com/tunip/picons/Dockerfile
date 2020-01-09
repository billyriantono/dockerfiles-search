FROM alpine:3.6

COPY ./usr/local/bin/build-picons.sh /usr/local/bin/build-picons.sh

RUN apk add --no-cache \
        ca-certificates \
        coreutils \
        shadow \
        tzdata && \
    useradd -u 911 -U -d /config -s /bin/false abc && \
    usermod -G users abc && \
    apk update && \
    apk add --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/community \
        bash \
        binutils \
        curl \
        findutils \
        git \
        imagemagick \
        jq \
        librsvg \
        pngquant \
        tar \
        util-linux \
        xz && \
    rm -rf /var/cache/apk/* /tmp/* && \
    chmod +x /usr/local/bin/build-picons.sh
    
