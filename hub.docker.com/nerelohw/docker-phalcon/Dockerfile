FROM nerelohw/docker-php7
MAINTAINER Hongshun Yang<wholerencom@gmail.com>


ENV CPHALCON_VERSION 3.4.1
ENV CPHALCON_DOWNLOAD_URL https://github.com/phalcon/cphalcon/archive/v$CPHALCON_VERSION.tar.gz

RUN apk add -U --virtual build-deps autoconf build-base linux-headers git \ 
&& cd /tmp/ \
&& wget -qO- $CPHALCON_DOWNLOAD_URL | tar xvz \
&& cd cphalcon-$CPHALCON_VERSION/build/ \
&& ./install \
&& cd ~ \
&& rm -rf /tmp/* \
&& apk del -U build-deps \
&& rm -rf /var/cache/apk/* 

RUN echo "extension=phalcon.so" > /etc/php7/conf.d/phalcon.ini
