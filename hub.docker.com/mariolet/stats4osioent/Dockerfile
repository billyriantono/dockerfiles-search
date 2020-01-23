FROM alpine:edge

# Upgrade default packages
RUN apk update && apk upgrade

# Set workers log directory
ENV LOG_DIR=/var/log/workers

# Set custom time zone info
ENV TZ=Europe/Moscow
RUN apk add --no-cache tzdata

# Install PHP 7
RUN apk add --no-cache php7 php7-pear php7-dev \
    php7-pdo php7-pdo_mysql php7-pdo_pgsql php7-pdo_sqlite \
    php7-mbstring php7-tokenizer php7-xml php7-simplexml \
    php7-zip php7-opcache php7-iconv php7-intl php7-pcntl \
    php7-json php7-gd php7-ctype php7-pecl-oauth \
    php7-pecl-redis php7-pecl-apcu php7-pecl-imagick php7-dom \
    php7-pecl-memcached php7-ftp php7-imap php7-xmlwriter \
    php7-exif php7-sqlite3 php7-curl php7-bcmath

# PHP 7 MongoDB support
RUN apk --update add --virtual build-dependencies build-base openssl-dev autoconf && \
    pecl install mongodb && \
    pecl clear-cache && \
    echo "exwtension=mongodb.so" > /etc/php7/conf.d/mongodb.ini && \
    apk del build-dependencies build-base openssl-dev autoconf && \
    rm -rf /var/cache/apk/*

# Supervisor manager install
RUN apk add --no-cache supervisor

# Change supervisor mode in config file
RUN sed -i 's/;nodaemon=false/nodaemon=true/g' /etc/supervisord.conf

# PHP Configuration
COPY ./php/php.ini /etc/php7/php.ini

# Supervisor processes
RUN mkdir ${LOG_DIR} -p
COPY ./procs  /etc/supervisor.d

# Container initialization script
COPY ./bin/init.sh /usr/local/bin/init

# Copy default app sources
COPY ./app /var/www/app

VOLUME ["/var/www/app", "/etc/supervisor.d"]
WORKDIR ${LOG_DIR}

ENTRYPOINT ["init"]