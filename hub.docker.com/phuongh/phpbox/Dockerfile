FROM alpine:3.3
MAINTAINER Phuong <phuonghuynh.net@gmail.com>

# Add s6-overlay
ENV S6_OVERLAY_VERSION v1.16.0.1

RUN echo 'http://dl-6.alpinelinux.org/alpine/v3.3/main' > /etc/apk/repositories && \
    apk update && apk add bind-tools bash nginx ca-certificates git curl \
    php-fpm php-json php-zlib php-xml php-pdo php-phar php-openssl \
    php-pdo_mysql php-mysqli php-bcmath php-opcache php-ctype php-curl \
    php-gd php-iconv php-mcrypt php-sockets \
    openssl python py-pip supervisor hiredis hiredis-dev tzdata \
    # build packages
    php-dev build-base autoconf automake openssl-dev libevent-dev pcre-dev && \
    mv /etc/php/conf.d/sockets.ini /etc/php/conf.d/00-sockets.ini && \

    # add s6
    curl -sSL https://github.com/just-containers/s6-overlay/releases/download/${S6_OVERLAY_VERSION}/s6-overlay-amd64.tar.gz \
    | tar xvfz - -C / && \

    # update timezone
    cp /usr/share/zoneinfo/Asia/Saigon /etc/localtime && echo 'Asia/Saigon' > /etc/timezone && \

    pip install pika && \

    # build mongodb extension
    cd /tmp && \
    wget https://pecl.php.net/get/mongo-1.6.12.tgz && \
    tar xzf mongo-* && \
    cd mongo-* && \
    phpize && ./configure && make && make install && \
    echo 'extension=mongo.so' > /etc/php/conf.d/mongo.ini && \

    # build libevent
    cd /tmp && \
    wget https://pecl.php.net/get/libevent-0.1.0.tgz && \
    tar xzf libevent-* && \
    cd libevent-* && phpize && ./configure && make && make install && \
    echo 'extension=libevent.so' > /etc/php/conf.d/22-libevent.ini && \

    # build phpiredis
    cd /tmp && \
    git clone https://github.com/nrk/phpiredis.git phpiredis && \
    cd phpiredis && phpize && ./configure && make && make install && \
    echo 'extension=phpiredis.so' > /etc/php/conf.d/33-phpiredis.ini && \

    # remote build package
    apk del php-dev build-base autoconf automake openssl-dev pcre-dev py-pip git tzdata && \
    rm -rf /var/cache/apk/* /tmp/*

EXPOSE 80
ADD root /
RUN chmod 0755 /init.sh
CMD ["/init.sh"]
