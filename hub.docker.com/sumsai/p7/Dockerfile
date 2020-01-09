FROM sumsai/php7:latest

RUN DEBIAN_FRONTEND="noninteractive" \
    && yum update -y \
    && yum install -y curl zip \
    && curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && chmod a+x /usr/local/bin/composer \
    && yum clean packages\
    && rm -rf /var/lib/apt/lists/*

CMD php -v && composer -V
