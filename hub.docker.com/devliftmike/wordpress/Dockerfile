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
  php7-fpm \
  php7-json \
  php7-zlib \
  php7-xml \
  php7-pdo \
  php7-phar \
  php7-openssl \
  php7-pdo_mysql \
  php7-mysqli \
  php7-session \
  php7-gd \
  php7-iconv \
  php7-mcrypt \
  php7-curl \
  php7-opcache \
  php7-ctype \
  php7-apcu \
  php7-intl \
  php7-bcmath \
  php7-mbstring \
  php7-dom \
  php7-xmlreader \
  php7-simplexml \
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

ADD config/nginx.conf /etc/nginx/
ADD config/php-fpm.conf /etc/php7/
ADD config/run.sh /
RUN chmod +x /run.sh

EXPOSE 80
VOLUME ["/DATA"]

CMD ["/run.sh"]