## Stage 0
FROM alpine:latest as builder

## Set Versions to download
ARG NGINX_VERSION=1.15.8
ARG NGINX_RTMP_VERSION=1.2.1

## Get the following packages
RUN apk update \
    && apk add \
           curl \
           gcc \
           git \
           libc-dev \
           libstdc++ \
           make \
           openssl \
           openssl-dev \
           pcre \
           pcre-dev \
           zlib-dev \
    && cd /tmp \
    && curl --remote-name http://nginx.org/download/nginx-${NGINX_VERSION}.tar.gz \
    && git clone https://github.com/arut/nginx-rtmp-module.git -b v${NGINX_RTMP_VERSION} \
    && tar xzf nginx-${NGINX_VERSION}.tar.gz \
    && cd nginx-${NGINX_VERSION} \
    && ./configure \
          --add-module=../nginx-rtmp-module \
          --prefix=/opt/nginx \
          --with-http_ssl_module \
          --with-debug \
          --with-cc-opt="-Wimplicit-fallthrough=0" \
    && make \
    && make install

## Stage 1
FROM alpine:latest
RUN apk update \
    && apk add \
           ca-certificates \
           libstdc++ \
           openssl \
           pcre

## Copy from Stage 0
COPY --from=0 /opt/nginx /opt/nginx
COPY --from=0 /tmp/nginx-rtmp-module/stat.xsl /opt/nginx/conf/stat.xsl

## Delete exiting nginx config
RUN rm /opt/nginx/conf/nginx.conf

## Add run script to system
ADD run.sh /

## Expose the following ports
EXPOSE 1935
EXPOSE 8080

## Start here
CMD ["/run.sh"]