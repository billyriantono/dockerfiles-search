FROM ubuntu:18.04
MAINTAINER Flyrainning "http://www.fengpiao.net"

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update -y \
  && apt-get install -y \
    openssl \
    nginx \
    php-fpm \
    php-cli \
    php-imagick \
    php-json \
    php-services-json \
    php-mail \
    php-mbstring \
    php-memcached \
    php-mongodb \
    php-redis \
    php-xml \
    php-zip \
    php-ssh2 \
    php-curl \
    php-gd \
    php-mysql \
    php-odbc \
    php-sqlite3 \
    php-xmlrpc \
    php-sybase \
    php-amqp \
    php-geos \
    php-http-request \
    php-log \
    php-markdown \
    php-net-socket \
    php-pgsql \
    php-yaml \
    php-pear \
    php-dev \
    librdkafka-dev \
  && apt-get autoclean \
  && apt-get autoremove \
  && rm -rf /var/lib/apt/lists/*

ADD etc /etc
ADD app /app
ADD bin /bin

RUN pecl install rdkafka
RUN echo extension=rdkafka.so > /etc/php/7.2/mods-available/rdkafka.ini
RUN ln /etc/php/7.2/mods-available/rdkafka.ini /etc/php/7.2/fpm/conf.d/20-rakafka.ini


WORKDIR /app
RUN chmod a+x /bin/start.sh /bin/install.sh
RUN /bin/install.sh

ENV VERSION 1
ENV PATH "/app:$PATH"

EXPOSE 80
ENTRYPOINT ["/bin/start.sh"]
