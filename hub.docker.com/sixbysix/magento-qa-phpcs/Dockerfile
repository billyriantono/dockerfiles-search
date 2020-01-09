FROM php:7.0

RUN apt-get update && apt-get install -y unzip git-core

RUN curl https://getcomposer.org/installer | php && mv composer.phar /usr/local/bin/composer

COPY composer.json /composer.json
COPY phpcs.xml /phpcs.xml

RUN composer update
RUN chmod -R 777 /vendor/squizlabs/php_codesniffer/
COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

COPY php.ini /usr/local/etc/php/

WORKDIR /app
ENTRYPOINT ["/entrypoint.sh"]