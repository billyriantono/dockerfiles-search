FROM alpine:3.4
MAINTAINER Connor Poole <connor.poole@gmail.com>

RUN apk add --no-cache bash inotify-tools ca-certificates su-exec curl curl-dev libcurl libcap openssl wget \
    && wget -O /usr/local/bin/dumb-init https://github.com/Yelp/dumb-init/releases/download/v1.2.0/dumb-init_1.2.0_amd64 \
    && chmod +x /usr/local/bin/dumb-init \
    && apk del --purge deps; bash -c "rm -rf /{tmp,root}/{*,.??*}" \
    && rm -rf /var/cache/apk/*

