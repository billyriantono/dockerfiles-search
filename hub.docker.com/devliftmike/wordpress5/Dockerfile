FROM alpine:3.6
LABEL maintainer="Devlift <info@devlift.com>"
ADD VERSION .

ENV USER_ID=100 USER_GID=101 SMTP_HOST=mail SMTP_PORT=1025

RUN echo 'http://dl-4.alpinelinux.org/alpine/latest-stable/main' >> /etc/apk/repositories\
  && apk update \
  && apk add --no-cache \
  bash \
  less \
  vim \
  nginx \
  ca-certificates \
  php5-fpm \
  php5-json \
  php5-zlib \
  php5-xml \
  php5-pdo \
  php5-phar \
  php5-openssl \
  php5-pdo_mysql \
  php5-mysqli \
  php5-gd \
  php5-iconv \
  php5-mcrypt \
  php5-curl \
  php5-opcache \
  php5-ctype \
  php5-intl \
  php5-bcmath \
  php5-dom \
  php5-xmlreader \
  mysql-client \
  openssh-client \
  git \
  curl \
  rsync \
  musl \
  && apk --update --no-cache add tar
RUN echo http://dl-2.alpinelinux.org/alpine/edge/community/ >> /etc/apk/repositories
RUN apk --no-cache add shadow
RUN rm -rf /var/cache/apk/*

ENV TERM="xterm" \
  DB_HOST="172.17.0.1" \
  DB_NAME="" \
  DB_USER=""\
  DB_PASS=""

ENV PATH /DATA/bin:$PATH

RUN ln -s /usr/bin/php5 /usr/bin/php

ADD config/nginx.conf /etc/nginx/
ADD config/php-fpm.conf /etc/php5/
ADD config/run.sh /
RUN chmod +x /run.sh

EXPOSE 80
VOLUME ["/DATA"]

CMD ["/run.sh"]